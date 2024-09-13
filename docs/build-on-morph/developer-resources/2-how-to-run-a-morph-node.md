---
title: Comment Exécuter un Noeud Morph
lang: fr-FR
---

## Exécuter un Noeud Complet Morph 

Ce guide décrit les étapes pour démarrer un noeud Morph. L'exemple suppose que le répertoire personnel est `~/.morph` 

### Exigences matérielles

L'exécution du noeud Morph nécessite 2 processus : `geth` et `node`.  

- `Geth` : la couche d'exécution Morph qui doit respecter les [exigences matérielles de go-ethereum](https://github.com/ethereum/go-ethereum#hardware-requirements), mais avec moins de stockage, 500 Go suffisent jusqu'à présent. 

- `Node` : la couche de consensus Morph intégrée de Tendermint qui doit respecter les [exigences matérielles de Tendermint](https://docs.tendermint.com/v0.34/tendermint-core/running-in-production.html#processor-and-memory). 

:::tip
En raison des limitations de l'implémentation actuelle de geth, seul le mode archive est pris en charge, ce qui signifie que la taille de stockage augmentera continuellement avec les blocs produits.
:::

### Construire le binaire exécutable

#### Cloner Morph

```
mkdir -p ~/.morph 
cd ~/.morph
git clone https://github.com/morph-l2/morph.git
```

Actuellement, nous utilisons la balise v0.2.0-beta comme notre version bêta.

```
cd morph
git checkout v0.2.0-beta
```

#### Construire Geth

Remarque : Vous avez besoin d'un compilateur C pour construire geth.

```
make nccc_geth
```

#### Construire Node

```
cd ~/.morph/morph/node 
make build
```

### Synchroniser depuis le bloc de genèse

#### Préparation de la configuration

Téléchargez les fichiers de configuration et créez le répertoire de données.

```
cd ~/.morph
wget https://raw.githubusercontent.com/morph-l2/config-template/main/holesky/data.zip
unzip data.zip
```

Créez un secret partagé avec le noeud.

```
cd ~/.morph
openssl rand -hex 32 > jwt-secret.txt
```

#### Script pour démarrer le processus

*Geth*

```
./morph/go-ethereum/build/bin/geth --morph-holesky \
    --datadir "./geth-data" \
    --http --http.api=web3,debug,eth,txpool,net,engine \
    --authrpc.addr localhost \
    --authrpc.vhosts="localhost" \
    --authrpc.port 8551 \
    --authrpc.jwtsecret=./jwt-secret.txt \
    --miner.gasprice="100000000" \
    --log.filename=./geth.log
```


*tail -f geth.log* pour vérifier si Geth fonctionne correctement, ou vous pouvez également exécuter la commande curl ci-dessous pour vérifier si vous êtes connecté au pair.


```
curl -X POST -H 'Content-Type: application/json' --data 
'{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":74}' 
localhost:8545

{"jsonrpc":"2.0","id":74,"result":"0x3"}
```


*Node*

```
./morph/node/build/bin/morphnode --home ./node-data \
     --l2.jwt-secret ./jwt-secret.txt \
     --l2.eth http://localhost:8545 \
     --l2.engine http://localhost:8551 \
     --log.filename ./node.log
```


tail -f node.log pour vérifier si le noeud fonctionne correctement, et vous pouvez également exécuter la commande curl pour vérifier l'état de connexion de votre noeud.


```
curl http://localhost:26657/net_info

{
  "jsonrpc": "2.0",
  "id": -1,
  "result": {
    "listening": true,
    "listeners": [
      "Listener(@)"
    ],
    "n_peers": "3",
    "peers": [
      {
        "node_info": {
          "protocol_version": {
            "p2p": "8",
            "block": "11",
            "app": "0"
          },
          "id": "0fb5ce425197a462a66de015ee5fbbf103835b8a",
          "listen_addr": "tcp://0.0.0.0:26656",
          "network": "chain-morph-holesky",
          "version": "0.37.0-alpha.1",
          "channels": "4020212223386061",
          "moniker": "morph-dataseed-node-1",
          "other": {
            "tx_index": "on",
            "rpc_address": "tcp://0.0.0.0:26657"
          }
        },
        "is_outbound": true,
```

### Vérifier l'état de synchronisation


curl http://localhost:26657/status to check the sync status of the node

```
{
  "jsonrpc": "2.0",
  "id": -1,
  "result": {
    "node_info": {
      "protocol_version": {
        "p2p": "8",
        "block": "11",
        "app": "0"
      },
      "id": "b3f34dc2ce9c4fee5449426992941aee1e09670f",
      "listen_addr": "tcp://0.0.0.0:26656",
      "network": "chain-morph-holesky",
      "version": "0.37.0-alpha.1",
      "channels": "4020212223386061",
      "moniker": "my-morph-node",
      "other": {
        "tx_index": "on",
        "rpc_address": "tcp://0.0.0.0:26657"
      }
    },
    "sync_info": {
      "latest_block_hash": "71024385DDBEB7B554DB11FD2AE097ECBD99B2AF826C11B2A74F7172F2DEE5D2",
      "latest_app_hash": "",
      "latest_block_height": "2992",
      "latest_block_time": "2024-04-25T13:48:27.647889852Z",
      "earliest_block_hash": "C7A73D3907C6CA34B9DFA043FC6D4529A8EAEC8F059E100055653E46E63F6F8E",
      "earliest_app_hash": "",
      "earliest_block_height": "1",
      "earliest_block_time": "2024-04-25T09:06:30Z",
      "catching_up": false
    },
    "validator_info": {
      "address": "5FB3D3734640792F14B70E7A53FBBD39DB9787A8",
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "rzN67ZJWsaLSGGpNj7HOWs8nrL5kr1n+w0OckWUCetw="
      },
      "voting_power": "0"
    }
  }
}
```

Le "catching_up" retourné indique si le nœud est synchronisé ou non. Vrai signifie qu'il est synchronisé. Pendant ce temps, le "latest_block_height" retourné indique la hauteur du dernier bloc que ce nœud a synchronisé.









