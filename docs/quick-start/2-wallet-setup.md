---
title: Configuration du Portefeuille
lang: fr-FR
keywords: [morph, ethereum, rollup, couche 2, preuve de validité, zk-rollup optimiste]
description: Améliorez votre expérience blockchain avec Morph - la solution de zk-rollup optimiste sécurisée, décentralisée, rentable et performante. Essayez-le maintenant !
---

## Portefeuille

Pour interagir avec les dApps sur Morph, vous avez besoin d'un portefeuille compatible. Voici quelques exemples de portefeuilles et des conseils de configuration.

<!--
### Portefeuille Bitget

À définir
-->

### MetaMask

- **Installation :** MetaMask peut être installé depuis leur [site officiel](https://metamask.io/download/).
- **Importation des configurations :** Pour configurer MetaMask pour le Testnet Morph, cliquez sur le bouton "ajouter au portefeuille" sur la page [https://explorer-holesky.morphl2.io/](Morph Holesky block explorer). Cela importera automatiquement l'ID de la chaîne et les URL RPC pour le Testnet Morph.
- **Utilisation du Testnet Ethereum Holesky :** Le Testnet Morph utilise le testnet Ethereum Holesky comme L1 sous-jacent, qui est déjà configuré par défaut dans MetaMask. Pour y accéder, activez "Afficher/masquer les réseaux de test" dans le menu déroulant de sélection du réseau MetaMask.

### Configuration manuelle du réseau

Actuellement, les liens "Ajouter au portefeuille" peuvent ne pas être compatibles avec tous les portefeuilles. Si vous rencontrez des problèmes pour les utiliser, vous devrez peut-être ajouter manuellement le Testnet Holesky et Morph en insérant les détails de configuration du tableau ci-dessous :

#### Configuration du réseau

| Nom                       | URL RPC                                | ID de la chaîne | Explorateur de blocs             | Symbole |
|--------------------------|----------------------------------------|------------------|----------------------------------|---------|
| Testnet Morph Holesky    | https://rpc-quicknode-holesky.morphl2.io | 2810             | https://explorer-holesky.morphl2.io | ETH     |
| Ethereum Holesky        | https://ethereum-holesky-rpc.publicnode.com/ | 17000            | https://holesky.etherscan.io     | ETH     |

Vous pouvez également visiter [chainlist](https://chainlist.org/?chain=11155111&search=morph&testnets=true) pour ajouter le testnet Morph et le testnet Ethereum.
