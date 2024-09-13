---
title: Exécuter un nœud Morph complet avec Docker
lang: fr-FR
---

Ce guide vous aidera à démarrer un nœud complet s'exécutant dans le conteneur Docker.

## Démarrage rapide

Actuellement, les utilisateurs doivent construire eux-mêmes l'image Docker en utilisant le fichier Docker et le fichier Docker Compose que nous fournissons. Cependant, il n'est pas nécessaire de s'inquiéter, car vous n'avez besoin que d'une seule commande pour démarrer rapidement un nœud complet. Cette commande s'occupera de tout pour vous, y compris le téléchargement des instantanés, la structuration des données et des fichiers de configuration, la construction de l'image et le démarrage du conteneur.

1. Clonez le dépôt du dockerfile

```bash
git clone --branch release/v0.2.x https://github.com/morph-l2/morph.git
```
2. Exécutez la commande suivante


```bash
cd ops/publicnode
make run-holesky-node
```

L'exécution de cette commande créera un répertoire `.morph-holesky` dans votre répertoire utilisateur par défaut, servant de répertoire principal du nœud. Avant de démarrer le nœud, cette commande effectuera plusieurs préparations :

- Créer le répertoire principal du nœud et copier les fichiers de configuration par défaut à l'intérieur.
- Préparer le fichier `secret-jwt.txt`pour l'authentification lors des appels RPC entre geth et le nœud.
- Télécharger les données d'instantané les plus récentes pour accélérer la synchronisation du nœud.
- Placer les données d'instantané extraites dans le dossier correspondant au sein du répertoire principal.

Après avoir terminé ces préparations, la commande construira automatiquement l'image et démarrera le conteneur, avec des volumes Docker montés sur le répertoire principal du nœud créé.


:::info
Si c'est votre première exécution, ces processus peuvent prendre un certain temps. Notez que si vous démarrez le nœud pour la première fois mais que vous avez déjà un répertoire `.morph-holesky` vous devez supprimer ce répertoire avant d'exécuter la commande. Sinon, la phase de préparation sera sautée, ce qui peut empêcher le nœud de fonctionner correctement.

Si la commande échoue pendant l'exécution, vous devrez également supprimer le répertoire `.morph-holesky`  précédemment créé avant de redémarrer.
:::

## Utilisation avancée

Avec le guide [Quick Start](#quick-start) ci-dessus, vous pouvez rapidement démarrer un nœud en utilisant les fichiers de configuration par défaut. Cependant, nous supportons également la personnalisation du répertoire principal du nœud et des paramètres.

### Personnalisation du répertoire de données

Les chemins des répertoires hôtes qui sont montés par le conteneur Docker sont spécifiés dans le fichier ```ops/publicnode/.env```.

```js title="ops/publicnode/.env"
// le dossier principal de votre nœud Morph
NODE_HOME=${HOME}/.morph-holesky 
// le répertoire de données pour votre client d'exécution : geth
GETH_DATA_DIR=${NODE_HOME}/geth-data
// le répertoire de données pour votre client de consensus : tendermint
NODE_DATA_DIR=${NODE_HOME}/node-data
// le script shell d'entrée pour démarrer le client d'exécution
GETH_ENTRYPOINT_FILE=${NODE_HOME}/entrypoint-geth.sh
// le fichier secret jwt pour communiquer entre le client d'exécution et le client de consensus via l'API engine
JWT_SECRET_FILE=${NODE_HOME}/jwt-secret.txt
// le nom de l'instantané pour le nœud Morph holesky 
SNAPSHOT_NAME=snapshot-20240805-1
```

Vous avez la flexibilité de personnaliser les chemins des répertoires selon vos besoins. Veuillez noter que si vous souhaitez exécuter **make run-holesky-node** pour générer les fichiers de configuration nécessaires et les instantanés pour faire fonctionner le nœud, vous devez vous assurer que le répertoire principal du nœud spécifié est nouveau (non créé précédemment) et ne pas modifier les chemins pour  ```GETH_DATA_DIR``` et ```NODE_DATA_DIR```.

### Personnalisation des paramètres

La configuration par défaut requise pour le démarrage du nœud se trouve dans le répertoire ```ops/publicnode/holesky``` Si votre répertoire principal du nœud est vide, la commande **run** copiera automatiquement ces fichiers de configuration dans le répertoire monté dans le conteneur Docker du nœud.

```javascript
└── holesky
    ├── entrypoint-geth.sh
    ├── geth-data
    │   └── static-nodes.json
    └── node-data
        ├── config
        │   ├── config.toml
        │   └── genesis.json
        └── data
```

Si vous souhaitez modifier la commande de démarrage de Geth, vous pouvez le faire en éditant le fichier ```entrypoint-geth.sh```Pour les ajustements des paramètres de configuration liés à Tendermint, vous devez modifier le fichier node-data/config/config.toml. Notez que si vous avez personnalisé votre ```GETH_DATA_DIR``` et ```NODE_DATA_DIR```, vous devrez placer manuellement les fichiers de configuration modifiés aux emplacements appropriés.

#### Gestion des instantanés (snapshot) vous-même


Vous pouvez également gérer manuellement les instantanés, en particulier si vous utilisez des chemins personnalisés pour les répertoires du nœud. La commande **make download-and-decompress-snapshot** dans le répertoire ```ops/publicnode``` vous aidera à télécharger et à décompresser l'archive d'instantané.

Ensuite, vous devez placer manuellement les fichiers de données décompressés dans les répertoires de données du nœud appropriés. Par exemple, si le dossier instantané s'appelle  ```snapshot-20240805-1```, déplacez le contenu de ```snapshot-20240805-1/geth``` vers le répertoire ```${GETH_DATA_DIR}/geth``` et le contenu de ```snapshot-20240805-1/data``` vers le répertoire ```${NODE_DATA_DIR}/data```.