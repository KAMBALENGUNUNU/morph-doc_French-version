---
title: Mettre à jour le nœud exécuté depuis Docker
lang: fr-FR
---

Si vous exécutez le conteneur Docker pour le nœud avec une configuration personnalisée, vous devrez mettre à jour l'image Docker vous-même, puis redémarrer le conteneur.

Le code source est disponible sur https://github.com/morph-l2/morph.git. Vous devez passer à la dernière version du code, puis mettre à jour votre image Docker.

Si vous utilisez [Exécuter un nœud Morph avec Docker](../2-how-to-run-a-morph-node-docker.md) pour démarrer le conteneur Docker, vous pouvez suivre les étapes suivantes pour mettre à jour le nœud.

### Étape 1 : Récupérer la dernière version du code

```bash
git clone https://github.com/morph-l2/morph.git
## vérifier la dernière version du code source dont vous avez besoin
git checkout ${latestVersion}
```
### Étape 2 : Arrêter les nœuds et supprimer les images précédentes

```bash
## arrêter le conteneur Docker
cd ops/publicnode
make stop-holesky-node
make rm-holesky-node
## supprimer l'image Docker précédente pour le nœud
docker rmi morph/node:latest
## supprimer l'image Docker précédente pour geth
docker rmi morph/geth-nccc:latest
```

### Étape 3 : Construire la dernière image et redémarrer le conteneur

:::note 
Veuillez noter que nous devons nous assurer que les paramètres de démarrage du conteneur Docker sont cohérents avec ceux utilisés auparavant. Si vous avez utilisé une configuration personnalisée auparavant, assurez-vous que la configuration et les chemins de répertoire utilisés dans cette exécution sont les mêmes qu'auparavant. Pour plus de détails, veuillez consulter [**Advanced Usage**](../2-how-to-run-a-morph-node-docker.md#advanced-usage) 
:::

```bash
## démarrer le conteneur Docker, il construira automatiquement les nouvelles images Docker
make run-holesky-node
```

