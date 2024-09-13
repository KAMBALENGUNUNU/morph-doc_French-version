---
title: Exécuter un Nœud Complet Morph depuis le Source
lang: fr-FR
---

Ce guide décrit les étapes pour démarrer un nœud Morph. L'exemple suppose que le répertoire personnel est `~/.morph`

## Exigences matérielles

L'exécution du nœud Morph nécessite 2 processus : `geth` et `node`.

- `Geth` : la couche d'exécution de Morph qui doit répondre aux [exigences matérielles de go-ethereum](https://github.com/ethereum/go-ethereum#hardware-requirements), mais avec moins de stockage, 500 Go suffisent pour l'instant.

- `Node` : la couche de consensus de Morph intégrée tendermint qui doit répondre aux [exigences matérielles de tendermint](https://docs.tendermint.com/v0.34/tendermint-core/running-in-production.html#processor-and-memory).

:::tip
Selon les limitations de l'implémentation actuelle de geth, nous ne supportons que le mode archive pour lancer Geth. Ainsi, la taille de stockage de Geth augmentera constamment avec les blocs produits.
:::

## Construire le binaire exécutable

### Cloner Morph

```
mkdir -p ~/.morph 
cd ~/.morph
git clone https://github.com/morph-l2/morph.git
```

Actuellement, nous utilisons le tag v0.2.0-beta comme notre version bêta.

```
cd morph
git checkout v0.2.0-beta
```

### Construire Geth

Remarque : Vous avez besoin d'un compilateur C pour construire geth.

```
make nccc_geth
```

### Construire Node

```
cd ~/.morph/morph/node 
make build
```

## Préparation de la Configuration

1. Téléchargez les fichiers de configuration et créez le répertoire de données.

```
cd ~/.morph
wget https://raw.githubusercontent.com/morph-l2/config-template/main/holesky/data.zip
unzip data.zip
```

2. Créez un secret partagé avec le nœud.

```
cd ~/.morph
openssl rand -hex 32 > jwt-secret.txt
```

## Synchroniser à partir d'un snapshot(Recommandé)

Vous devez d'abord construire le binaire et préparer les fichiers de configuration dans les étapes ci-dessus, puis télécharger l'instantané.

### Télécharger le snapshot

```bash
## télécharger le paquet
wget -q --show-progress https://snapshot.morphl2.io/holesky/snapshot-20240805-1.tar.gz
## décompresser le paquet
tar -xzvf snapshot-20240805-1.tar.gz
```

Extraire les données de l'instantané dans le répertoire de données auquel votre nœud fait référence.


```bash
mv snapshot-20240805-1/geth geth-data
mv snapshot-20240805-1/data node-data
```

### Démarrer le client d'exécution

```bash
./morph/go-ethereum/build/bin/geth --morph-holesky \
    --datadir "./geth-data" \
    --http --http.api=web3,debug,eth,txpool,net,engine \
    --authrpc.addr localhost \
    --authrpc.vhosts="localhost" \
    --authrpc.port 8551 \
    --authrpc.jwtsecret=./jwt-secret.txt \
    --log.filename=./geth.log
```

Utilisez tail -f geth.log pour vérifier si Geth fonctionne correctement, ou vous pouvez également exécuter la commande curl ci-dessous pour vérifier si vous êtes connecté au pair.


```Shell
curl -X POST -H 'Content-Type: application/json' --data '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":74}' localhost:8545

{"jsonrpc":"2.0","id":74,"result":"0x3"}
```

Démarrer le client de consensus

```Bash
 ./morph/node/build/bin/morphnode --home ./node-data \
     --l2.jwt-secret ./jwt-secret.txt \
     --l2.eth http://localhost:8545 \
     --l2.engine http://localhost:8551 \
     --log.filename ./node.log 
```

Utilisez tail -f node.log pour vérifier si le nœud fonctionne correctement, et vous pouvez également exécuter la commande curl pour vérifier l'état de connexion de votre nœud.

```Bash
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
 ....... 
 ```

### Vérifier l'état de synchronisation

Utilisez http://localhost:26657/status pour vérifier l'état de synchronisation du nœud.

```Bash
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

Le retour de "catching_up" indique si le nœud est synchronisé ou non. *True* signifie qu'il est synchronisé. Meanwhile, the returned  latest_block_height indicates the latest block height this node synced.

## Synchroniser à partir du bloc de genèse (Non Recommandé)

Démarrez le client d'exécution et le client de consensus directement sans télécharger l'instantané.

