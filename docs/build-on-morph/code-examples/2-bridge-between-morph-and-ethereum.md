---
title: Pont entre Morph et Ethereum
lang: fr-FR
keywords: [morph,ethereum,rollup,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution de rollup optimiste zk sécurisée, décentralisée, rentable et performante. Essayez-le maintenant !
---

## Pont d'un ERC20 à travers une passerelle personnalisée

## Étape 1 : Lancez un token sur Holesky

Tout d'abord, nous avons besoin d'un token à relier. Il n'est pas nécessaire d'avoir une mise en œuvre particulière d'ERC20 pour qu'un token soit compatible avec L2. Si vous avez déjà un token, n'hésitez pas à passer cette étape. Si vous souhaitez déployer un nouveau token, utilisez le contrat suivant d'un simple token ERC20 qui émet 1 million de tokens au déployeur lors du lancement.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract L1Token est ERC20 {
  constructor() ERC20("Mon Token L1", "MTL1") {
    _mint(msg.sender, 1_000_000 ether);
  }
}

```

## Étape 2 : Lancez le token correspondant sur le testnet Morph Holesky

Ensuite, vous lancerez un équivalent de ce token sur Morph, qui représentera le token original sur Holesky. Ce token peut mettre en œuvre une logique personnalisée pour correspondre à celle du token L1 ou même ajouter des fonctionnalités supplémentaires au-delà de celles du token L1.

Pour que cela fonctionne :

- Le token doit mettre en œuvre l'interface `IMorphStandardERC20`pour être compatible avec le pont.
- Le contrat doit fournir l'adresse de la passerelle et les adresses des tokens correspondants (le token L1 que nous venons de lancer) dans les fonctions `gateway()` et `counterpart()`Il doit également permettre à la passerelle L2 d'appeler les fonctions `mint()` et `burn()`du token, qui sont appelées lorsqu'un token est déposé et retiré.

Voici un exemple complet d'un token compatible avec le pont. Dans le constructeur, vous passerez l'adresse de la passerelle personnalisée Morph (`0x058dec71E53079F9ED053F3a0bBca877F6f3eAcf`) et l'adresse du token lancé sur Holesky.

```solidity// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@Morph-tech/contracts@0.1.0/libraries/token/IMorphERC20Extension.sol";

contract L2Token est ERC20, IMorphERC20Extension {
  // Nous stockons la passerelle et l'adresse du token L1 pour fournir les fonctions gateway() et counterpart() qui sont nécessaires à l'interface Morph Standard ERC20
  address _gateway;
  address _counterpart;

  // Dans le constructeur, nous passons comme paramètres la passerelle personnalisée L2 et l'adresse du token L1
  constructor(address gateway_, address counterpart_) ERC20("Mon Token L2", "MTL2") {
    _gateway = gateway_;
    _counterpart = counterpart_;
  }

  function gateway() public view returns (address) {
    return _gateway;
  }

  function counterpart() external view returns (address) {
    return _counterpart;
  }

  // Nous permettons la création de tokens uniquement à la Passerelle afin qu'elle puisse émettre de nouveaux tokens lorsqu'ils sont reliés depuis L1
  function transferAndCall(address receiver, uint256 amount, bytes calldata data) external returns (bool success) {
    transfer(receiver, amount);
    data;
    return true;
  }

  // Nous permettons la création de tokens uniquement à la Passerelle afin qu'elle puisse émettre de nouveaux tokens lorsqu'ils sont reliés depuis L1
  function mint(address _to, uint256 _amount) external onlyGateway {
    _mint(_to, _amount);
  }

  // De même que pour la création, la Passerelle peut brûler des tokens lorsqu'ils sont reliés de L2 à L1
  function burn(address _from, uint256 _amount) external onlyGateway {
    _burn(_from, _amount);
  }

  modifier onlyGateway() {
    require(gateway() == _msgSender(), "Ownable: l'appelant n'est pas la passerelle");
    _;
  }
}

```
## Étape 3 : Ajoutez le jeton au Morph Bridge

Vous devez contacter l'équipe Morph pour ajouter le jeton au contrat `L2CustomERC20Gateway` dans Morph et au contrat `L1CustomERC20Gateway` dans L1. De plus, suivez les instructions sur le dépôt [token lists](https://github.com/Morph-tech/token-list) pour ajouter votre jeton à l'interface officielle du pont Morph.

## Étape 4 : Déposez des jetons

Une fois que votre jeton a été approuvé par l'équipe Morph, vous devriez pouvoir déposer des jetons depuis L1. Pour ce faire, vous devez d'abord approuver l'adresse du contrat `L1CustomGateway` sur Holesky (`0x31C994F2017E71b82fd4D8118F140c81215bbb37`). Ensuite, déposez des jetons en appelant la fonction `depositERC20` du contrat `L1CustomGateway`. Cela peut être fait en utilisant [notre interface du pont](https://Morph.io/bridge), [Etherscan Holesky](https://Holesky.etherscan.io/address/0x31C994F2017E71b82fd4D8118F140c81215bbb37#writeProxyContract), ou un contrat intelligent.

## Étape 5 : Retirez des jetons

Vous suivrez des étapes similaires pour renvoyer des jetons de L2 à L1. Tout d'abord, approuvez l'adresse `L2CustomGateway` (`0x058dec71E53079F9ED053F3a0bBca877F6f3eAcf`) puis retirez les jetons en appelant la fonction `withdrawERC20` du contrat `L2CustomGateway`.

## Envoyez des messages entre Morph et Ethereum

## Déploiement des contrats

### Contrat intelligent cible

Commençons par déployer le contrat intelligent cible. Nous allons utiliser le contrat Greeter pour cet exemple, mais vous pouvez utiliser n'importe quel autre contrat. Déployez-le sur Holesky ou Morph. Sur Morph, L1 et L2 utilisent la même API, donc c'est à vous de choisir.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

// Ce contrat Greeter sera interagi via le MorphMessenger à travers le pont
contract Greeter {
  string public greeting = "Hello World!";

  // Cette fonction sera appelée par executeFunctionCrosschain sur le contrat intelligent Operator
  function setGreeting(string memory greeting_) public {
    greeting = greeting_;
  }
}
```

Nous allons maintenant exécuter `setGreeting`de manière inter-chaînes.

### Contrat intelligent Operator

Changez de chaîne et déployez le `GreeterOperator`. Donc, si vous avez déployé le contrat `Greeter` sur L1, déployez le `GreeterOperator` sur L2 ou vice versa.

```solidity// SPDX-License-Identifier: MIT
pragma solidity ^0.8.16;

// L'interface Morph Messenger est la même sur L1 et L2, elle permet d'envoyer des transactions inter-chaînes
// Importons-la directement depuis la bibliothèque des contrats Morph
import "@Morph-tech/contracts@0.1.0/libraries/IMorphMessenger.sol";

// Le GreeterOperator est capable d'exécuter la fonction Greeter à travers le pont
contract GreeterOperator {
  // Cette fonction exécutera setGreeting sur le contrat Greeter
  function executeFunctionCrosschain(
    address MorphMessengerAddress,
    address targetAddress,
    uint256 value,
    string memory greeting,
    uint32 gasLimit
  ) public payable {
    IMorphMessenger MorphMessenger = IMorphMessenger(MorphMessengerAddress);
    // sendMessage peut exécuter n'importe quelle fonction en encodant l'abi en utilisant la fonction encodeWithSignature
    MorphMessenger.sendMessage{ value: msg.value }(
      targetAddress,
      value,
      abi.encodeWithSignature("setGreeting(string)", greeting),
      gasLimit,
      msg.sender
    );
  }
}

```

## Appeler une fonction inter-chaînes

Nous passons le message en exécutant `executeFunctionCrosschain` et en passant les paramètres suivants :

- `MorphMessengerAddress`: Cela dépendra d'où vous avez déployé le contrat `GreeterOperator`.
  - Si vous l'avez déployé sur Holesky, utilisez `0x50c7d3e7f7c656493D1D76aaa1a836CedfCBB16A`. Si vous l'avez déployé sur Morph Holesky, utilisez `0xBa50f5340FB9F3Bd074bD638c9BE13eCB36E603d`.
- `targetAddress`:  L'adresse du contrat `Greeter` sur la chaîne opposée.
- `value`: Dans ce cas, c'est `0` car `setGreeting`n'est pas payable.
- `greeting`:  C'est le paramètre qui sera envoyé à travers le message. Essayez de passer `“This message was cross-chain!”`
- `gasLimit`:
  - Si vous envoyez le message de L1 à L2, une limite de gaz d'environ `1000000`devrait être plus que suffisante. Cela dit, si vous fixez cela trop haut, et que  `msg.value` ne couvre pas `gasLimit` * `baseFee`,la transaction sera annulée. Si `msg.value` est supérieur aux frais de gaz, la portion non utilisée sera remboursée.
   - Si vous envoyez le message de L2 à L1, passez  `0`, car la transaction sera complétée en exécutant une transaction supplémentaire sur L1.

### Relayer le message lors de l'envoi de L2 à L1

Lorsqu'une transaction est passée de L2 à L1, une "exécution de transaction de retrait" supplémentaire doit être envoyée sur L1. Pour ce faire, vous devez appeler  `relayMessageWithProof` sur le contrat L1 Morph Messenger depuis un portefeuille EOA.

Vous pouvez le faire directement sur [Etherscan Holesky](https://Holesky.etherscan.io/address/0x50c7d3e7f7c656493d1d76aaa1a836cedfcbb16a#writeProxyContract#F3).

Pour ce faire, vous devrez passer une preuve d'inclusion Merkle pour la transaction transférée et d'autres paramètres. Vous les interrogez en utilisant l'API Morph Bridge.

{/* TODO: finir d'examiner les problèmes d'API */}

Nous finalisons les spécificités de l'API, mais pour l'instant, récupérez ou utilisez curl pour accéder à l'endpoint suivant :

```bash
curl "https://Holesky-api-bridge.Morph.io/api/claimable?page_size=10&page=1&address=GREETER_OPERATOR_ADDRESS_ON_L2"
```

<!--
 Remplacez `GREETER_OPERATOR_ADDRESS_ON_L2` par l'adresse de votre contrat GreeterOperator tel que lancé sur L2. Lisez-en plus sur les transactions d'exécution de retrait dans l'article sur le [Morph Messenger](/developers/l1-and-l2-bridging/the-Morph-messenger).
-->
:::tip
  Cette API a été créée pour notre interface de pont. Elle n'est pas encore finalisée et pourrait changer à l'avenir. Nous mettrons à jour ce guide lorsque l'API sera finalisée.
:::

:::tip Quiconque peut exécuter votre message
  `relayMessageWithProof` est entièrement sans autorisation, donc tout le monde peut l'appeler en votre nom s'il est prêt à payer les frais de gaz L1. Cette fonctionnalité permet d'ajouter une infrastructure de support supplémentaire, y compris des outils pour automatiser ce processus pour les applications et les utilisateurs.
:::

Après avoir exécuté et confirmé la transaction sur L1 et L2, le nouvel état de `greeting` dans le contrat `Greeter` devrait être `“Ce message a été transféré entre chaînes!”`. Envoyer un message d'une chaîne à l'autre devrait prendre environ 20 minutes après que les transactions soient confirmées sur la chaîne d'origine.

Félicitations, vous avez maintenant exécuté une transaction d'une chaîne à l'autre en utilisant notre pont natif !
