# How to use bootstrap.dat

## What is bootstrap.dat?

`bootstrap.dat` is a file that contains the copy of blockchain from genesis block to a certain point of time. This compressed `bootstrap.dat` file is used to speed up the initial blockchain download times. Your wallet client downloads and verifies each block from the P2P network. This is usually slow and especially if you are using wallet for the first time, then syncing process can take quite a long time.

Instead of using peer to peer communication your wallet client can read blockchain data from this compressed bootstrap file which contains the copy of blockchain data until a certain block height. Once the wallet client completes reading data from bootstrap file, it will then use the P2P connection to download the remaining blocks. This method is faster and moreover it consumes less bandwidth compared to standard synchronization process. However still bootstrap method takes some time as your wallet client needs to validate each individual blocks.

## How to generate bootstrap.dat?

Construct a linear, no-fork, best version of the Qtum blockchain. The scripts run using Python 3 but are compatible with Python 2.

### Step 1: Download script files

Clone the qtum official repo and enter `contrib/linearize` directory

    git clone https://github.com/qtumproject/qtum.git
    cd qtum/contrib/linearize

### Step 2: Download hash list

    ./linearize-hashes.py linearize.cfg > hashlist.txt

Required configuration file settings for linearize-hashes:
* RPC: `datadir` (Required if `rpcuser` and `rpcpassword` are not specified)
* RPC: `rpcuser`, `rpcpassword` (Required if `datadir` is not specified)

Optional config file setting for linearize-hashes:
* RPC: `host`  (Default: `127.0.0.1`)
* RPC: `port`  (Default: `3889`)
* Blockchain: `min_height`, `max_height`
* `rev_hash_bytes`: If true, the written block hash list will be byte-reversed. (In other words, the hash returned by getblockhash will have its bytes reversed.) False by default. Intended for generation of standalone hash lists but safe to use with linearize-data.py, which will output the same data no matter which byte format is chosen.

The `linearize-hashes` script requires a connection, local or remote, to a JSON-RPC server. Running `qtumd` or `qtum-qt -server` will be sufficient.

### Step 3: Copy local block data

    ./linearize-data.py linearize.cfg

Required configuration file settings:
* `output_file`: The file that will contain the final blockchain. or
* `output`: Output directory for linearized `blocks/blkNNNNN.dat` output.

Optional config file setting for linearize-data:
* `debug_output`: Some printouts may not always be desired. If true, such output will be printed.
* `file_timestamp`: Set each file's last-accessed and last-modified times, respectively, to the current time and to the timestamp of the most recent block written to the script's blockchain.
* `genesis`: The hash of the genesis block in the blockchain.
* `input`: qtumd blocks/ directory containing blkNNNNN.dat
* `hashlist`: text file containing list of block hashes created by linearize-hashes.py.
* `max_out_sz`: Maximum size for files created by the `output_file` option. (Default: `1000*1000*1000` bytes)
* `netmagic`: Network magic number.
* `out_of_order_cache_sz`: If out-of-order blocks are being read, the block can be written to a cache so that the blockchain doesn't have to be sought again. This option specifies the cache size. (Default: `100*1000*1000` bytes)
* `rev_hash_bytes`: If true, the block hash list written by linearize-hashes.py will be byte-reversed when read by linearize-data.py. See the linearize-hashes entry for more information.
* `split_timestamp`: Split blockchain files when a new month is first seen, in addition to reaching a maximum file size (`max_out_sz`).

## How to use bootstrap.dat

1. Download `bootstrap.dat` file from `https://s.qtum.site/bootstrap.dat`.
2. Move `bootstrap.dat` into qtum data directory, the default datadir paths are different paths for different OS:
   * Linux: `~/.qtum`
   * OSX: `~/Library/Application Support/Qtum`
   * Windows: `%APPDATA%\Qtum` (Please paste this path to your windows explorer, the path will be resolved automatically)
3. Restart wallet and wait for reindexing.
