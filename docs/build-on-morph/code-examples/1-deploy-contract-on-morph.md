---
title: Déployer des contrats sur Morph
lang: fr-FR
keywords: [morph,ethereum,rollup,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution optimiste zk-rollup sécurisée, décentralisée et rentable. Essayez-le maintenant !
---

Le réseau de test Morph Holesky permet à quiconque de déployer un contrat intelligent sur Morph. Ce tutoriel vous guidera dans le déploiement d'un contrat sur Morph Holesky en utilisant des outils de développement Ethereum courants.

Ce [dépôt de démonstration](https://github.com/morph-l2/morph-examples/tree/main/contract-deployment-demos) illustre le déploiement de contrats avec [Hardhat](https://hardhat.org/) et [Foundry](https://github.com/foundry-rs/foundry).

:::tip
  Avant de commencer à déployer le contrat, vous devez demander des jetons de test à un robinet Holesky et utiliser le
  [pont](https://bridge-holesky.morphl2.io) pour transférer des ETH de test de _Holesky_ à _Morph Holesky_. 
  
  Consultez notre [robinet](../../quick-start/3-faucet.md) pour plus de détails.
:::

<!--

## Déployer des contrats avec Remix

-->

## Déployer avec Hardhat

### Cloner le dépôt

```bash
git clone https://github.com/morph-l2/morph-examples.git
```

### Installer les dépendances

Si ce n'est pas déjà fait, installez [nodejs](https://nodejs.org/en/download/) et [yarn](https://classic.yarnpkg.com/lang/en/docs/install).

```bash
cd contract-deployment-demos/hardhat-demo
yarn install
```
Cela installera tout ce dont vous avez besoin, y compris Hardhat pour vous.



### Compiler

Compilez votre contrat


```bash
yarn compile
```

### Tester

Cela exécutera le script de test dans test/Lock.ts


```bash
yarn test
```

### Déployer

 Créez un fichier `.env` en suivant l'exemple de `.env.example` dans le répertoire racine. Changez `PRIVATE_KEY` par votre propre clé privée de compte dans le `.env`.

Et changez les paramètres du réseau dans le fichier hardhat.config.ts avec les informations suivantes :

   ```javascript
    morphTestnet: {
      url: process.env.MORPH_TESTNET_URL || "",
      accounts:
        process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [],
    }
   ```
Ensuite, exécutez la commande suivante pour déployer le contrat sur le réseau de test Morph Holesky. Cela exécutera le script de déploiement qui définit les paramètres initiaux ; vous pouvez modifier le script dans scripts/deploy.ts.

```bash
yarn deploy:morphTestnet
```

### Vérifiez vos contrats sur Morph Explorer

Pour vérifier votre contrat via Hardhat, vous devez ajouter les configurations Etherscan et Sourcify suivantes à votre fichier hardhat.config.js :


```javascript
module.exports = {
  networks: {
    morphTestnet: { ... }
  },
  etherscan: {
    apiKey: {
      morphTestnet: 'anything',
    },
    customChains: [
      {
        network: 'morphTestnet',
        chainId: 2810,
        urls: {
          apiURL: 'https://explorer-api-holesky.morphl2.io/api? ',
          browserURL: 'https://explorer-holesky.morphl2.io/',
        },
      },
    ],
  },
};
```
Ensuite, exécutez la commande de vérification hardhat pour terminer la vérification

```bash
npx hardhat verify --network morphTestnet DEPLOYED_CONTRACT_ADDRESS <ConstructorParameter>
```

Parr example

```bash
npx hardhat verify --network morphTestnet 0x8025985e35f1bAFfd661717f66fC5a434417448E '0.00001'
```


Une fois réussi, vous pouvez vérifier votre contrat et la transaction de déploiement sur [Morph Holesky Explorer](https://explorer-holesky.morphl2.io)
   

## Déployer des contrats avec Foundry


### Cloner le dépôt

```bash
git clone https://github.com/morph-l2/morph-examples.git
```

### Installer Foundry

```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

Ensuite, allez dans le bon dossier de notre exemple :


```bash
cd contract-deployment-demos/foundry-demo
```

### Compiler

```bash
forge build
```
### Déployer


Un script de déploiement et l'utilisation de variables d'environnement ont déjà été configurés pour vous. Vous pouvez voir le script dans script/Counter.s.sol

Renommez votre fichier .env.example en .env et remplissez votre clé privée. L'URL RPC a déjà été remplie ainsi que l'URL du vérificateur.

Pour utiliser les variables dans votre fichier .env, exécutez la commande suivante :

```shell
source .env
```

Vous pouvez maintenant déployer sur Morph avec la commande suivante :


```shell
forge script script/Counter.s.sol --rpc-url $RPC_URL --broadcast --private-key $DEPLOYER_PRIVATE_KEY --legacy
```

Ajustez au besoin pour vos propres noms de script.


### Vérifier

La vérification nécessite certains drapeaux passés au script de vérification normal. Vous pouvez vérifier en utilisant la commande ci-dessous :

```bash
 forge verify-contract YourContractAddress Counter\
  --chain 2810 \
  --verifier-url $VERIFIER_URL \
  --verifier blockscout --watch
```

Une fois réussi, vous pouvez vérifier votre contrat et la transaction de déploiement sur  [Morph Holesky Explorer](https://explorer-holesky.morphl2.io).


## Questions et commentaires

Merci de participer et de développer sur le réseau de test Morph Holesky ! Si vous rencontrez des problèmes, rejoignez notre [Discord](https://discord.com/invite/L2Morph) et retrouvez-nous dans le canal #dev-support.


