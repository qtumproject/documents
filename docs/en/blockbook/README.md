# How to Set up blockbook for Qtum



**Blockbook** is an [address](https://wiki.trezor.io/Address) or [account](https://wiki.trezor.io/Account) balance backend (or blockchain indexer) for [Trezor Wallet](https://wiki.trezor.io/Trezor_Wallet).

It's pretty much the backend for trezor and apparently, truswallet.

To set it up, I basically followed this tutorial: <https://wiki.trezor.io/User_manual:Running_a_local_instance_of_Trezor_Wallet_backend_(Blockbook)>

However, there's some specific topics not mentioned in this tutorial:

1. Blockbook uses a lot of disk space, the minimum disk size on the server should be around 30GB, 60GB recommended for long term growth.

2. Blockbook, along with qtum-core, requires at least 4GB ram to function, 8GB and higher is recommended (our deployment server has 3GB ram plus a 5GB swap file)

3. Even with 8GB ram, it's recommended to have swap enabled on the server

   

   

   ## How to create a 5GB swap file and activate it (do this as root)

```
dd if=/dev/zero of=/swapfile bs=1M count=5120 
```

```
chmod 600 /swapfile
```

```
mkswap /swapfile
```

```
 swapon /swapfile
```

```
echo "swapfile none swap defaults 0 0" >> /etc/fstab
```



Ok, now that we're done creating the swap file and made sure we have at least 30GB disk space, then we can follow the rest of the steps as posted on https://wiki.trezor.io/User_manual:Running_a_local_instance_of_Trezor_Wallet_backend_(Blockbook)

## Ports opened by blockbook

Blockbook creates several ports for Qtum when running, those ports are: 

| blockbook internal port | blockbook public port | backend rpc port | backend service ports (zmq) |
| ----------------------- | --------------------- | ---------------- | --------------------------- |
| 9088                    | 9188                  | 8088             | 38388                       |

To be able to access blockbook externally, we need to make port 9188 accessible via a back-proxy on nginx, here's how:

## Setting up nginx web server for blockbook

Blockbook has a web UI with information about the qtum blockchain, just like on https://blockbook.qtum.info

SSL cert needed, if we don't have one, we can just create one with letsencrypt but we won't go into details in this doc.

Here's the Nginx config I'm using for blockbook.qtum.info


    server {
        listen 80;
        listen 443 ssl http2;
          ssl_certificate /etc/letsencrypt/live/blockbook.qtum.info/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/blockbook.qtum.info/privkey.pem; # managed by Certbot
        include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
        
        server_name blockbook.qtum.info;
    
    # force https-redirects
    if ($scheme = http) {
        return 301 https://blockbook.qtum.info$request_uri;
    }
    
    location / {
        proxy_pass https://localhost:9188;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
    
        # Enables WS support
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_redirect off;
    }
    }
We need to make sure the following ports are open in order for this to function correctly:

9188 443 80 