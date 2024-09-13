---
title: Comprendre le Coût des Transactions sur Morph
lang: fr-FR
keywords: [morph,ethereum,rollup,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution zk-rollup optimiste, décentralisée, sécurisée et performante. Essayez-la maintenant !
---

Les frais de transaction sur Morph fonctionnent de manière similaire à ceux d'Ethereum. Cependant, la Layer 2 introduit certains aspects uniques. Le zkEVM optimiste de Morph rend ces différences faciles à comprendre et encore plus faciles à gérer.

Cette page inclut la formule pour calculer le coût en gas des transactions sur Morph.  
Il existe deux types de coûts pour les transactions sur Morph : les frais d'exécution L2 et les frais de données/sécurité L1.

<!--
:::tip

Les frais de transaction sont collectés dans le solde du contrat `SequencerFeeVault`. Ce contrat suit également le montant que nous avons historiquement retiré vers L1 en utilisant `totalProcessed()(uint256)`.

Le producteur de blocs ne reçoit aucune récompense directe, et l'opcode `COINBASE` renvoie l'adresse du coffre de frais.

:::
-->

## Les frais d'exécution L2

Comme sur Ethereum, les transactions sur Morph entraînent des coûts en gas pour l'utilisation de la computation et du stockage.

Chaque transaction sur L2 paiera des **frais d'exécution**, égaux à la quantité de gas utilisée multipliée par le prix du gas de la transaction.

Morph prend en charge le type de transaction EIP-1559. Le modèle de tarification EIP-1559, qui comprend des frais de base et des frais prioritaires, contribue à des frais de transaction plus prévisibles et stables.

La formule est simple :

```
l2_execution_fee = l2_gas_price * l2_gas_used
l2_gas_price = l2_base_fee + l2_priority_fee
```


La quantité de gas utilisée sur L2 dépend de la transaction spécifique. En raison de la compatibilité avec l'EVM, la consommation de gas sur Morph est généralement similaire à celle d'Ethereum.

## Les frais de données L1

Les transactions sur Morph sont également publiées sur Ethereum, ce qui est crucial pour la sécurité de Morph, car cela garantit que toutes les données nécessaires pour vérifier l'état de Morph sont toujours disponibles publiquement sur Ethereum.

Les utilisateurs doivent payer pour le coût de soumission de leurs transactions sur Ethereum, ce que l'on appelle les frais de données L1. Ces frais représentent généralement la majeure partie du coût total d'une transaction sur Morph.

Formule :

```
l1DataFee = (l1BaseFee * commitScalar + l1BlobBaseFee * tx_data_gas * blobScalar) / rcfg.Precision
```

où tx_data_gas is

```
tx_data_gas = count_zero_bytes(tx_data) * 4 + count_non_zero_bytes(tx_data) * 16
```

Et les autres paramètres :

1. l1BaseFee : Frais de base sur Layer1
2. commitScalar : un facteur utilisé pour mesurer le coût en gas de l'engagement des données
3. l1BlobBaseFee : le blobBaseFee sur L1
4. blobScalar : un facteur utilisé pour mesurer le coût en gas d'une transaction stockée dans un blob EIP-4844


:::tip
Vous pouvez lire les valeurs des paramètres depuis le contrat oracle des prix du gas. Morph a pré-déployé `GasPriceOracle`, accessible sur Morph Holesky à [GasPriceOracle](https://explorer-holesky.morphl2.io/address/0x530000000000000000000000000000000000000F).
:::

## Effet des frais de transaction sur le développement logiciel

### Envoi de transactions

Le processus d'envoi d'une transaction sur Morph est identique à celui sur Ethereum.

Lorsque vous envoyez une transaction, vous devez fournir un prix du gas qui est supérieur ou égal au prix actuel du gas sur L2.

Comme sur Ethereum, vous pouvez interroger ce prix du gas avec la méthode RPC `eth_gasPrice`.

De même, vous devez définir la limite de gas de votre transaction de la même manière que vous le feriez sur Ethereum (par exemple via `eth_estimateGas`).


### Affichage des frais aux utilisateurs

De nombreuses applications Ethereum affichent des frais estimés aux utilisateurs en multipliant le prix du gas par la limite de gas.

Cependant, comme mentionné précédemment, les utilisateurs sur Morph paient à la fois des frais d'exécution L2 et des frais de données L1.

Par conséquent, vous devez afficher la somme de ces deux frais pour donner aux utilisateurs l'estimation la plus précise du coût total d'une transaction.


#### Estimation des frais d'exécution L2

Vous pouvez estimer les frais d'exécution L2 en multipliant le prix du gas par la limite de gas, comme sur Ethereum.

#### [Estimation des frais de données L1](./understand-transaction-cost-on-morph#the-l1-data-fee)


#### Estimation des frais totaux

Vous pouvez estimer les frais totaux en combinant vos estimations des frais d'exécution L2 et des frais de données L1.

### Envoi du maximum d'ETH

L'envoi du montant maximum d'ETH qu'un utilisateur possède dans son portefeuille est un cas d'utilisation relativement courant.

Lorsque vous faites cela, vous devrez soustraire les frais d'exécution L2 estimés et les frais de données L1 estimés du montant d'ETH que vous souhaitez que l'utilisateur envoie.

Utilisez la logique décrite ci-dessus pour estimer les frais totaux.

## Erreurs RPC courantes

### Fonds insuffisants

- Code d'erreur : `-32000`
- Message d'erreur : `transaction invalide : fonds insuffisants pour l1Fee + l2Fee + value`

Vous obtiendrez cette erreur lorsque vous tentez d'envoyer une transaction et que vous n'avez pas assez d'ETH pour payer la valeur de la transaction, les frais d'exécution L2 et les frais de données L1.  
Vous pourriez rencontrer cette erreur en essayant d'envoyer le maximum d'ETH si vous ne prenez pas correctement en compte à la fois les frais d'exécution L2 et les frais de données L1.

### Prix du gas trop bas

- Code d'erreur : `-32000`
- Message d'erreur : `prix du gas trop bas : X wei, utilisez au moins tx.gasPrice = Y wei`

Ceci est une erreur RPC personnalisée que Morph renvoie lorsqu'une transaction est rejetée parce que le prix du gas est trop bas.  
Voir la section sur [Répondre aux mises à jour du prix du gas](#responding-to-gas-price-updates) pour plus d'informations.

### Prix du gas trop élevé

- Code d'erreur : `-32000`
- Message d'erreur : `prix du gas trop élevé : X wei, utilisez au maximum tx.gasPrice = Y wei`

Ceci est une erreur RPC personnalisée que Morph renvoie lorsqu'une transaction est rejetée parce que le prix du gas est trop élevé.  
Nous incluons cela comme une mesure de sécurité pour empêcher les utilisateurs d'envoyer accidentellement une transaction avec un prix du gas L2 extrêmement élevé.  
Voir la section sur [Répondre aux mises à jour du prix du gas](#responding-to-gas-price-updates) pour plus d'informations.
