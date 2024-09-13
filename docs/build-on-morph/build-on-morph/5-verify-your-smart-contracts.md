---
title: Vérifiez Vos Smart Contracts
lang: fr-FR
keywords: [morph,ethereum,rollup,couche2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution décentralisée, sécurisée, rentable et performante de type optimistic zk-rollup. Essayez-le maintenant !
---

Après avoir déployé vos smart contracts, il est crucial de vérifier votre code sur notre [explorateur de blocs](https://explorer-holesky.morphl2.io). Cela peut être automatisé en utilisant votre framework de développement, tel que Hardhat.

## Vérifier avec un framework de développement

La plupart des outils de smart contract disposent de plugins pour vérifier les contrats sur Etherscan. Blockscout prend en charge les APIs de vérification de contrat d'Etherscan, ce qui rend l'utilisation de ces outils facile avec le Testnet de Morph.

### Vérifier avec Hardhat

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

### Vérifier avec Foundry

La vérification avec Foundry nécessite quelques options supplémentaires à passer dans le script de vérification classique. Vous pouvez vérifier en utilisant la commande ci-dessous :

```bash
 forge verify-contract YourContractAddress Counter\
  --chain 2810 \
  --verifier-url https://explorer-api-holesky.morphl2.io/api? \
  --verifier blockscout --watch
```
## Vérifier avec l'interface de l'explorateur Morph

- Visitez : [Explorateur de blocs Morph](https://explorer-holesky.morphl2.io)

Nous supportons actuellement 6 différentes façons de vérifier vos contrats sur notre explorateur de blocs.

Il y a 2 paramètres généraux :

- Compilateur : Il doit être cohérent avec ce que vous sélectionnez lors du déploiement.
- Optimisation : Peut être ignoré si vous n'avez pas d'optimisation de contrat. Si vous en avez, elle doit être cohérente avec le déploiement.

### Méthode : Solidity (Code source aplati)

#### Interface :

![fscs](../../../assets/docs/dev/contract-verify/flatsourcesol.png)

#### Aplatir

Aplatissez via la [commande forge](https://book.getfoundry.sh/reference/forge/forge-flatten?highlight=flatten#forge-flatten), par exemple :

~~~bash
forge flatten --output FlattenedL2StandardBridge.sol ./contracts/L2/L2StandardBridge.sol
~~~

### Méthode : Solidity (Entrée JSON standard)

![sjis1](../../../assets/docs/dev/contract-verify/sjisol1.png)

#### Obtenir le fichier JSON

- Peut être obtenu via solc
- Peut être obtenu via le compilateur Remix

![sjis2](../../../assets/docs/dev/contract-verify/sjisol3.png)

![sjis3](../../../assets/docs/dev/contract-verify/sjisol3.png)

### Méthode : Solidity (Fichiers multiples)

#### Interface :

- Vous pouvez soumettre plusieurs fichiers de contrat selon vos besoins
![mpfs1](../../../assets/docs/dev/contract-verify/mpfsol.png)

#### Processus de fichier SOL
- S'il y a un fichier importé, il doit être modifié pour être référencé par un chemin au même niveau, et ces fichiers doivent être soumis ensemble. 
![mpfs2](../../../assets/docs/dev/contract-verify/mpfsol2.png)

### Méthode : Vyper (Contrats)

#### Interface :
![cv](../../../assets/docs/dev/contract-verify/cv.png)

### Méthode : Vyper (Entrée JSON standard)

#### Interface :
![sjiv](../../../assets/docs/dev/contract-verify/sjiv.png)

### Méthode : Vyper (Fichiers multiples)

#### Interface :
![mpfv](../../../assets/docs/dev/contract-verify/mpfv.png)

### Après vérification

![avp](../../../assets/docs/dev/contract-verify/avp.png)
