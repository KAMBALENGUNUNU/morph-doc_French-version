---
title: Pont entre Morph et Ethereum
lang: fr-FR
keywords: [morph,ethereum,rollup,couche2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution zk-rollup optimiste sécurisée, décentralisée, économique et performante. Essayez-le maintenant !
---

Veuillez d'abord consulter notre documentation sur [Communication entre Morph et Ethereum](../../how-morph-works/general-protocol-design/2-communicate-between-morph-and-ethereum.md) pour certaines connaissances de base requises.

## Déposer des ETH et des jetons ERC20 depuis L1​

Le **Gateway Router** permet le pontage d'ETH et de jetons ERC20 de L1 à L2 en utilisant respectivement les fonctions `depositETH` et `depositERC20`. C'est un pont sans autorisation déployé sur L1. Notez que les jetons ERC20 auront une adresse différente sur L2. Vous pouvez utiliser la fonction `getL2ERC20Address` pour interroger la nouvelle adresse.

:::tip
  Les fonctions **`depositETH`** et **`depositERC20`** sont des fonctions payantes. Le montant d'ETH envoyé à ces fonctions sera utilisé pour payer les frais sur L2. Si le montant n'est pas suffisant, la transaction ne sera pas envoyée. Tout excès d'ETH sera renvoyé à l'expéditeur. `0.00001 ETH` devrait être largement suffisant pour traiter un dépôt de jetons.
:::

Lors du pontage de jetons ERC20, vous n'avez pas à vous soucier de sélectionner le bon Gateway. En effet, le `L1GatewayRouter` choisira le bon point d'entrée sous-jacent pour envoyer le message :

- **`L1StandardERC20Gateway` :** Ce Gateway permet tout dépôt ERC20 et sera sélectionné par défaut par le `L1GatewayRouter` pour un jeton ERC20 qui n'a pas besoin de logique personnalisée sur L2. Lors du tout premier pontage de jetons, un nouveau jeton sera créé sur L2 implémentant le `MorphStandardERC20`. Pour pontage un jeton, appelez la fonction `depositERC20` sur le `L1GatewayRouter`.

<!---->
<!--
- **`L1CustomERC20Gateway` :** Ce Gateway sera sélectionné par le `L1GatewayRouter` pour les jetons avec une logique personnalisée. Pour qu'une paire de jetons L1/L2 fonctionne sur le pont Morph Custom ERC20, le contrat de jeton L2 doit implémenter `IMorphStandardERC20`. De plus, le jeton doit accorder la capacité de `mint` ou de `burn` au `L2CustomERC20Gateway`.
-->

Tous les contrats du Gateway formeront le message et l'enverront au `L1CrossDomainMessenger`, qui peut envoyer des messages arbitraires à L2. Le `L1CrossDomainMessenger` passe le message au `L1MessageQueueWithGasPriceOracle`. Tout utilisateur peut envoyer des messages directement au Messenger pour exécuter des données arbitraires sur L2.

Cela signifie qu'ils peuvent exécuter n'importe quelle fonction sur L2 à partir d'une transaction effectuée sur L1 via le pont. Bien qu'une application puisse directement transmettre des messages aux contrats de jetons existants, le Gateway abstrait les détails et simplifie les transferts et les appels.

Lorsqu'un nouveau bloc est créé sur L1, le **Sequencer** détectera le message sur le `L1MessageQueue` et soumettra la transaction à L2 via le nœud L2. Enfin, le nœud L2 transmettra la transaction au contrat `L2CrossDomainMessenger` pour exécution sur L2.

## Retirer des ETH et des jetons ERC20 depuis L2

Le Gateway L2 est très similaire au Gateway L1. Nous pouvons retirer des ETH et des jetons ERC20 vers L1 en utilisant les fonctions `withdrawETH` et `withdrawERC20`. L'adresse du contrat est déployée sur L2. Nous utilisons `getL1ERC20Address` pour récupérer l'adresse du jeton sur L1.

:::tip
  Les fonctions **`withdrawETH`** et **`withdrawERC20`** sont payantes. Le montant d'ETH envoyé à ces fonctions sera utilisé pour payer les frais sur L1. Si le montant n'est pas suffisant, la transaction ne sera pas envoyée. Tout excès d'ETH sera renvoyé à l'expéditeur. Les frais dépendront de l'activité sur L1, mais `0.005 ETH` devrait suffire pour traiter un retrait de jetons.
:::

:::tip
  **Assurez-vous que les transactions ne seront pas annulées sur L1 lors de l'envoi depuis L2**. Il n'est pas possible de récupérer les ETH, jetons ou NFT pontés si votre transaction échoue sur L1. Tous les actifs sont brûlés sur Morph lorsque la transaction est envoyée, et il est impossible de les créer à nouveau.
:::

### Finaliser votre Retrait

En plus de lancer une demande de retrait sur Morph, il y a une étape supplémentaire à effectuer. Vous devez finaliser votre retrait sur Ethereum.

En raison de la conception optimiste du zkEVM de Morph, vous pouvez lire les détails [ici](../../how-morph-works/general-protocol-design/2-communicate-between-morph-and-ethereum.md).

Pour ce faire, vous devez d'abord vous assurer :

- Que le lot contenant les transactions de retrait a passé la période de contestation et est marqué comme finalisé (c'est-à-dire dans le contrat `Rollup`, **withdrawalRoots[batchDataStore[_batchIndex].withdrawalRoot] = true**).

Une fois confirmé, vous pouvez appeler notre interface de services backend :

`/getProof?nonce=withdraw.index`

pour obtenir toutes les informations nécessaires à la finalisation de votre retrait, qui incluent :

- Index : La position de la transaction de retrait dans l'arbre de retrait, ou le rang de votre transaction parmi toutes les transactions L2->L1.
- Feuille : La valeur de hachage de votre transaction de retrait stockée dans l'arbre.
- Preuve : La preuve de Merkle de votre transaction de retrait.
- Racine : La racine de l'arbre de retrait.

Vous devez utiliser la fonction `proveAndRelayMessage` du contrat `L1CrossDomainMessenger`.

Après avoir obtenu les informations ci-dessus, la finalisation de l'opération de retrait peut être effectuée en appelant `L1CrossDomainMessenger.proveAndRelayMessage()`.

Les paramètres requis sont :

```solidity
  address _from, 
  address _to, 
  uint256 _value, 
  uint256 _nonce, 
  bytes memory _message, 
  bytes32[32] calldata _withdrawalProof, 
  bytes32 _withdrawalRoot
```

`_from`, `_to`, `_value`, `_nonce`, et `_message` sont le contenu original de la transaction de retrait, qui peut être obtenu à partir de l'événement `SentMessage` inclus dans la transaction initiée par le retrait de la couche L2.

`_withdrawalProof` et `_withdrawalRoot` peuvent être obtenus à partir de l'interface API backend mentionnée ci-dessus.

<!--

## Création d'un jeton ERC20 avec une logique personnalisée sur L2

Si un jeton nécessite une logique personnalisée sur L2, il devra être relié via un `L1CustomERC20Gateway` et un `L2CustomERC20Gateway` respectivement. Le jeton personnalisé sur L2 devra donner l'autorisation à la passerelle de créer de nouveaux jetons lors d'un dépôt et de brûler des jetons lors d'un retrait.

L'interface suivante est l'`IMorphStandardERC20` nécessaire pour déployer des jetons compatibles avec le `L2CustomERC20Gateway` sur L2.

```solidity
interface IMorphStandardERC20 {
  /// @notice Retourne l'adresse de la passerelle à laquelle le jeton appartient.
  function gateway() external view returns (address);

  /// @notice Retourne l'adresse du jeton contrepartie.
  function counterpart() external view returns (address);

  /// @dev Norme ERC677, voir https://github.com/ethereum/EIPs/issues/677
  /// Defi peut utiliser cette méthode pour transférer des jetons L1/L2 à L2/L1,
  /// et déposer sur le contrat L2/L1 en une seule transaction
  function transferAndCall(address receiver, uint256 amount, bytes calldata data) external returns (bool success);

  /// @notice Crée un certain nombre de jetons pour le compte du destinataire.
  /// @dev Outils de passerelle, seul le contrat de passerelle peut appeler cette fonction.
  /// @param _to L'adresse du destinataire.
  /// @param _amount Le montant du jeton à créer.
  function mint(address _to, uint256 _amount) external;

  /// @notice Brûle un certain nombre de jetons du compte.
  /// @dev Outils de passerelle, seul le contrat de passerelle peut appeler cette fonction.
  /// @param _from L'adresse du compte à partir duquel les jetons sont brûlés.
  /// @param _amount Le montant du jeton à brûler.
  function burn(address _from, uint256 _amount) external;
}
```
### Ajout d'un token ERC20 personnalisé sur L2 au Morph Bridge

Les tokens peuvent être transférés de manière sécurisée et sans autorisation via les contrats Gateway déployés par n'importe quel développeur. Cependant, Morph gère également un routeur ERC20 et une passerelle où tous les tokens créés par la communauté sont les bienvenus. Faire partie de la passerelle gérée par Morph signifie que vous n'aurez pas besoin de déployer les contrats Gateway, et votre token apparaîtra dans l'interface de Morph. Pour faire partie de la passerelle Morph, vous devez contacter l'équipe Morph pour ajouter le token aux contrats de pont sur L1 et L2. Pour cela, suivez les instructions dans le dépôt [token lists](https://github.com/Morph-tech/token-list) pour ajouter votre nouveau token à l'interface officielle de Morph.

-->


:::tip Utilisez le SDK

Vous pouvez également essayer notre SDK pour interagir avec le système de pont en vous référant à notre [documentation SDK](../sdk/globals.md).

:::

## Ajouter votre Token au Pont Officiel

Actuellement, notre pont officiel ne prend en charge que certains tokens prédéfinis. Si vous souhaitez transférer vos propres tokens, vous devez ajouter manuellement le token, et voici comment procéder.

### Ajouter des Tokens à la passerelle via l'interface Morph Bridge

La méthode la plus simple pour prendre en charge votre token est de l'ajouter manuellement sur notre [interface officielle de pont](https://bridge-holesky.morphl2.io/). Vous pouvez le faire simplement en suivant les étapes ci-dessous :

1. Cliquez sur le bouton de sélection des tokens sur Morph Holesky Bridge

![tokenlist1](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist1.png)

2. Entrez et confirmez l'adresse du contrat token Ethereum souhaité dans la section des tokens personnalisés

![tokenlist2](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist2.png)

3. Obtenez l'adresse du contrat token sur Layer 2 et confirmez-la.

![tokenlist3](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist3.png)

4. Maintenant, il est pris en charge et vous et d'autres utilisateurs pouvez commencer à transférer ce token !

![tokenlist4](../../../assets/docs/protocol/general/bridge/tokenlist/tokenlist4.png)

### Ajouter la prise en charge du token à l'interface du pont

En ajoutant votre token à la passerelle, vous et d'autres utilisateurs pouvez transférer le token en entrant l'adresse du token. Vous devez soumettre une PR à notre dépôt de pont si vous souhaitez que votre token apparaisse dans la liste des tokens sur l'interface de pont.

Vous pouvez trouver comment procéder dans le [dépôt morph list](https://github.com/morph-l2/morph-list).

Gardez à l'esprit que :
- Vous devez ajouter à la liste à la fois votre token sur L1 et sur L2.
- L'adresse du contrat token sur L2 est obtenue en ajoutant vos tokens via l'interface du pont Morph.

Voici un [exemple de PR commit](https://github.com/morph-l2/morph-list/pull/27/commits/228481db6b8d69b8f40e7369dae62722aa570eb7) pour référence.




