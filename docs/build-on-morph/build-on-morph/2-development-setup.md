---
title: Configuration de Développement
lang: fr-FR
keywords: [morph, ethereum, rollup, layer2, preuve de validité, optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution optimistic zk-rollup sécurisée, décentralisée, rentable et performante. Essayez-le maintenant !
---

# Commencez à Développer sur Morph

Développer sur Morph est aussi simple que de développer sur Ethereum.

Pour déployer des contrats sur une chaîne MorphL2, il vous suffit de définir le point de terminaison RPC de votre chaîne MorphL2 cible et de déployer en utilisant votre cadre de développement Ethereum préféré :

- [Hardhat](https://hardhat.org/)
- [Foundry](https://github.com/foundry-rs/foundry)
- [Brownie](https://eth-brownie.readthedocs.io/en/stable/)
- [Alchemy](https://docs.alchemy.com/reference/alchemy-sdk-quickstart)
- [QuickNode SDK](https://www.quicknode.com/docs/quicknode-sdk/getting-started?utm_source=morph-docs)

...tout fonctionne parfaitement !

# Testnet Holesky :

## Étape 1 : Configuration du Réseau

Avant de commencer, assurez-vous d'être connecté aux réseaux suivants :

| Nom du Réseau | Testnet Holesky Morph | Testnet Holesky |
| --- | --- | --- |
| URL RPC | https://rpc-quicknode-holesky.morphl2.io | https://ethereum-holesky-rpc.publicnode.com/ |
| ID de Chaîne | 2810 | 17000 |
| Symbole de la Monnaie | ETH | ETH |
| URL de l'Explorateur de Blocs | https://explorer-holesky.morphl2.io/ | https://holesky.etherscan.io/ |

:::tip Connexion Websocket

wss://rpc-quicknode-holesky.morphl2.io

:::

### Informations sur le Consensus Tendermint

RPC Tendermint : https://rpc-consensus-holesky.morphl2.io

Documentation RPC de Tendermint : https://docs.tendermint.com/v0.34/rpc/#/

## Étape 2 : Configurez votre cadre de développement

### Hardhat

Modifiez votre fichier de configuration Hardhat `hardhat.config.ts` pour pointer vers le RPC public de Morph.

```jsx
const config: HardhatUserConfig = {
  ...
  networks: {
    morphl2: {
      url: 'https://rpc-quicknode-holesky.morphl2.io',
      accounts:
        process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
      gasprice = 2000000000
    },
  },
};
```

### Foundry

Pour déployer en utilisant le RPC public de Morph, exécutez :

```jsx
forge create ... --rpc-url= --legacy
```



### ethers.js

Setting up a Morph  provider in an ethers script:

```jsx
import { ethers } from 'ethers';

const provider = new ethers.providers.JsonRpcProvider(
  'https://rpc-quicknode-holesky.morphl2.io'
);
```

## Étape 3 : Acquérir de l'Ether

Pour commencer à construire sur Morph, vous aurez peut-être besoin d'un peu d'ETH de testnet. Utilisez un robinet (faucet) pour obtenir de l'Ether Holesky, puis [bridge](https://bridge-holesky.morphl2.io)  l'Ether Ethereum de test vers le testnet Morph.

Chaque robinet a ses propres règles et exigences, vous devrez donc peut-être essayer plusieurs avant d'en trouver un qui fonctionne pour vous.

Sites Web des robinets Holesky ETH :

https://stakely.io/en/faucet/ethereum-holesky-testnet-eth

https://faucet.quicknode.com/ethereum/holesky

https://holesky-faucet.pk910.de/

https://cloud.google.com/application/web3/faucet/ethereum (nécessite un compte Google)

Nous avons notre propre[website faucet](https://morphfaucet.com/) qui peut réclamer de l'ETH & USDT pour votre utilisation initiale.


Morph propose également un [Discord faucet](../../quick-start/3-faucet.md#morph-holesky-eth) pour obtenir USDT Morph Holesky & ETH Morph Holesky.

Une fois que vous avez reçu de l'ETH sur Holesky, vous devriez le voir dans votre portefeuille sur le *réseau Holesky*. Cela peut prendre quelques secondes pour qu'il apparaisse, mais vous pouvez vérifier le statut en recherchant une transaction vers votre adresse sur un **[Holesky Block Explorer](https://holesky.etherscan.io/)**.


