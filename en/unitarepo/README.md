# Using UNITA official Repository on Ubuntu 16.04-19.04, Debian, Mint and Archlinux





We've published our official Unita repository on [https://repo.unita.network](https://repo.unita.network), this repository supports the following distributions:

### Debian

- 8.x (Jessie)
- 9.x (stretch)
- Testing (Buster)
- Unstable (Sid)

### Ubuntu 

16.04 - 19.04

### Mint 

18.x - 19x



### Archlinux

[Get it from the AUR](https://aur.archlinux.org/packages/qtum-core/) 



### Tutorial focus

This tutorial assumes you have a basic knowledge of Linux and terminal usage, the entire process uses the Linux terminal.



## Installing on Ubuntu

### Obtaining signing key

First, we need to obtain the Unita signing key from the ubuntu keyserver, here's how:

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys  BF5B197D`

This will download and add the Unita signing key to your Linux install.



### Adding repository to your APT sources.

`sudo su` - Sudo to root first

` echo "deb https://repo.unita.network/apt/ubuntu/ xenial main" >> /etc/apt/sources.list`

This will add the repository to your APT sources file. **NOTE:** Please remember to change "xenial" for your Ubuntu version codename <!--(for instance, Ubuntu 17.10 codename is artful, in this case you need to replace xenial for artful)-->



### Refreshing APT sources and installing Unita

`sudo apt update && sudo apt install unita`

By doing this, we'll update our sources and install Unita on our Ubuntu Box



## Installing on Debian

Obtaining the public key in Debian is a bit different, but not complicated

First, we need to make sure **sudo** is installed: 

Type `sudo su` and press enter, if you get a password prompt, then you can move on to obtaining the public key

### Installing sudo

Obtain admin privileges (su to root) and then type your admin user (root) password

Once you're logged in as "root" please type the following: `apt-get install sudo`

When sudo finishes installing, add your user to the sudo group: `gpasswd -a youruser sudo`
Logout and then log in again.

### Obtaining Public key

Install dirmngr first

`sudo apt install dirmngr`

````sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys  BF5B197D` ```

This downloads and installs the Unita public key

### Adding repository to your APT sources.

`sudo su` - Sudo to root first

` echo "deb https://repo.unita.network/apt/debian/ stretch main" >> /etc/apt/sources.list`

This will add the repository to your APT sources file. **NOTE:** Please remember to change "stretch" for your Debian version codename <!--(for instance, Debian 8.x codename is jessie, in this case you need to replace stretch for jessie)-->



### Refreshing APT sources and installing Unita

`sudo apt update && sudo apt install unita`

By doing this, we'll update our sources and install Unita on our Debian Box


### Launching Unita

Launching is simple, we just go to our applications menu and scrolldown/search for Unita 


