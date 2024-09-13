---
title: Mise à jour du nœud exécuté sur l'hôte
lang: fr-FR
---

La mise à jour du nœud est simple. Il suffit d'installer la nouvelle version du fichier exécutable du nœud et de remplacer la version précédente. Ensuite, arrêtez le nœud en cours d'exécution et redémarrez-le avec la version mise à jour. Le nœud utilisera automatiquement les données de votre ancien nœud et synchronisera les derniers blocs qui ont été minés depuis que vous avez arrêté l'ancien logiciel.

L'exécution du nœud nécessite deux fichiers binaires : `morphnode` et `geth`. Choisissez de mettre à jour les fichiers binaires en fonction de vos besoins spécifiques.

### Étape 1 : Compiler la nouvelle version du code

```bash
git clone https://github.com/morph-l2/morph.git
## vérifier la dernière version du code source dont vous avez besoin
git checkout ${latestVersion}
## installer geth
make nccc_geth
## installer morphnode
cd ./morph/node && make build
```

### Étape 2 : Arrêter les nœuds

```bash
## stop morphnode process
pid=`ps -ef | grep morphnode | grep -v grep | awk '{print $2}'`
kill  $pid

## stop geth process
pid=`ps -ef | grep geth | grep -v grep | awk '{print $2}'`
kill  $pid
```

### Étape 3 : Redémarrer

Assurez-vous d'utiliser la même commande de démarrage que vous avez utilisée avant la mise à jour

```bash
## start geth
./morph/go-ethereum/build/bin/geth --morph-holesky \
    --datadir "./geth-data" \
    --http --http.api=web3,debug,eth,txpool,net,engine \
    --authrpc.addr localhost \
    --authrpc.vhosts="localhost" \
    --authrpc.port 8551 \
    --authrpc.jwtsecret=./jwt-secret.txt \
    --log.filename=./geth.log

## start geth    
./morph/node/build/bin/morphnode --home ./node-data \
     --l2.jwt-secret ./jwt-secret.txt \
     --l2.eth http://localhost:8545 \
     --l2.engine http://localhost:8551 \
     --log.filename ./node.log 
```