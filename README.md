# Binance Smart Chain node Docker image

## QuickStart

Environment variable **NETWORK** possible values: ***mainnet***, ***testnet***

```
docker run -d \
    --name binance-smart-chain-node \
    -e NETWORK=mainnet \
    -v /data/bsc:/root \
    -p 8545:8545 \
    -p 8546:8546 \
    -p 6060:6060 \
    -p 30311:30311 \
    -p 30311:30311/udp \
        afanasjev/binance-smart-chain-node:latest --syncmode snap --cache 4096
```

Blockchain data will be stored at `/data/bsc` folder.

`config.toml` will be created if not exists at `/data/bsc/.ethereum/config.toml`

## Check sync status

```
docker exec binance-smart-chain-node bsc attach --exec eth.syncing

docker logs -f binance-smart-chain-node
```

## JSONRPC

* HTTP JSONRPC at port 8545
* WebSocket at 8546
* IPC (unix socket) at /data/bsc/.ethereum/geth.ipc

Test it using [geth_linux](https://github.com/binance-chain/bsc/releases) binary: 

```
geth_linux attach http://localhost:8545
geth_linux attach ws://localhost:8546
geth_linux attach /data/bsc/.ethereum/geth.ipc
# Last one needs root privileges
```

## More info

[original BSC repo](https://github.com/binance-chain/bsc)
