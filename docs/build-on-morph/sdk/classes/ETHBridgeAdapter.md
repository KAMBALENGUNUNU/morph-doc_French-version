[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / ETHBridgeAdapter

# Classe : ETHBridgeAdapter

Adaptateur de pont pour le pont ETH.

## Étend

- [`StandardBridgeAdapter`](StandardBridgeAdapter.md)

## Constructors

### new ETHBridgeAdapter()

> **new ETHBridgeAdapter**(`opts`): [`ETHBridgeAdapter`](ETHBridgeAdapter.md)

Crée une instance de StandardBridgeAdapter.

#### Paramètres

• **opts**

Options pour l'adaptateur.

• **opts.l1Bridge**: [`AddressLike`](../type-aliases/AddressLike.md)

Contrat du pont L1.

• **opts.l2Bridge**: [`AddressLike`](../type-aliases/AddressLike.md)

Contrat du pont L2.

• **opts.messenger**: [`CrossChainMessenger`](CrossChainMessenger.md)

Fournisseur utilisé pour faire des requêtes liées aux interactions entre chaînes.

#### Returne

[`ETHBridgeAdapter`](ETHBridgeAdapter.md)

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`constructor`](StandardBridgeAdapter.md#constructors)

#### Source

src/adapters/standard-bridge.ts:52

## Propriétés

### estimateGas

> **estimateGas**: `object`

Objet qui contient les fonctions qui estiment le gaz requis pour une transaction donnée.
Suit le modèle utilisé par ethers.js.

#### approve()

> **approve**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`BigNumber`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Retourne

`Promise`\<`BigNumber`\>

#### deposit()

> **deposit**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`BigNumber`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Retourne

`Promise`\<`BigNumber`\>

#### withdraw()

> **withdraw**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`BigNumber`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returne

`Promise`\<`BigNumber`\>

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`estimateGas`](StandardBridgeAdapter.md#estimategas)

#### Source

src/adapters/standard-bridge.ts:405

***

### l1Bridge

> **l1Bridge**: `Contract`

Contrat du pont L1.

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`l1Bridge`](StandardBridgeAdapter.md#l1bridge)

#### Source

src/adapters/standard-bridge.ts:41

***

### l2Bridge

> **l2Bridge**: `Contract`

Contrat du pont L2.

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`l2Bridge`](StandardBridgeAdapter.md#l2bridge)

#### Source

src/adapters/standard-bridge.ts:42

***

### messenger

> **messenger**: [`CrossChainMessenger`](CrossChainMessenger.md)

Fournisseur utilisé pour faire des requêtes liées aux interactions entre chaînes.

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`messenger`](StandardBridgeAdapter.md#messenger)

#### Source

src/adapters/standard-bridge.ts:40

***

### populateTransaction

> **populateTransaction**: `object`

Objet qui contient les fonctions qui génèrent des transactions à signer par l'utilisateur.
Suit le modèle utilisé par ethers.js.


#### approve()

> **approve**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`never`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returne

`Promise`\<`never`\>

#### deposit()

> **deposit**: (`l1Token`, `l2Token`, `amount`, `opts`) => `Promise`\<`TransactionRequest`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returne

`Promise`\<`TransactionRequest`\>

#### withdraw()

> **withdraw**: (`l1Token`, `l2Token`, `amount`, `opts`) => `Promise`\<`TransactionRequest`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Returne

`Promise`\<`TransactionRequest`\>

#### Remplace

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`populateTransaction`](StandardBridgeAdapter.md#populatetransaction)

#### Source

src/adapters/eth-bridge.ts:116

## Méthodes

### approbation()

> **approbation**(`l1Token`, `l2Token`, `opts`?): `Promise`\<`BigNumber`\>

Interroge le montant d'approbation du compte pour un jeton L1 donné.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`BigNumber`\>

Montant de jetons approuvés pour les dépôts depuis le compte.

#### Surcharges

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`approbation`](StandardBridgeAdapter.md#approbation)

#### Source

src/adapters/eth-bridge.ts:22

***

### approuver()

> **approuver**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

Approuve un dépôt dans la chaîne L2.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à approuver.

• **signer**: `Signer`

Signer utilisé pour signer et envoyer la transaction.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour la transaction d'approbation.

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`approuver`](StandardBridgeAdapter.md#approuver-2)

#### Source

src/adapters/standard-bridge.ts:250

***

### déposer()

> **déposer**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

Dépose des jetons dans la chaîne L2.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à déposer.

• **signer**: `Signer`

Signer utilisé pour signer et envoyer la transaction.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour la transaction de dépôt.

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`déposer`](StandardBridgeAdapter.md#déposer-2)

#### Source

src/adapters/standard-bridge.ts:262

***

### obtenirDépôtsParAdresse()

> **obtenirDépôtsParAdresse**(`adresse`, `opts`?): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Obtenez tous les dépôts pour une adresse donnée.

#### Paramètres

• **adresse**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse à rechercher pour les messages.

• **opts?**

Objet d'options.

• **opts.fromBlock?**: `BlockTag`

• **opts.toBlock?**: `BlockTag`

#### Retourne

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Tous les messages de pont de jetons de dépôt envoyés par l'adresse donnée.

#### Surcharges

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`obtenirDépôtsParAdresse`](StandardBridgeAdapter.md#getdepositsbyaddress)

#### Source

src/adapters/eth-bridge.ts:30

***

### obtenirRetraitesParAdresse()

> **obtenirRetraitesParAdresse**(`adresse`, `opts`?): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Obtenez toutes les retraites pour une adresse donnée.

#### Paramètres

• **adresse**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse à rechercher pour les messages.

• **opts?**

Objet d'options.

• **opts.fromBlock?**: `BlockTag`

• **opts.toBlock?**: `BlockTag`

#### Retourne

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Tous les messages de pont de jetons de retrait envoyés par l'adresse donnée.

#### Surcharges

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`obtenirRetraitesParAdresse`](StandardBridgeAdapter.md#getwithdrawalsbyaddress)

#### Source

src/adapters/eth-bridge.ts:64

***

### supportePaireJeton()

> **supportePaireJeton**(`l1Token`, `l2Token`): `Promise`\<`boolean`\>

Vérifie si la paire de jetons donnée est supportée par le pont.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

#### Retourne

`Promise`\<`boolean`\>

Si la paire de jetons donnée est supportée par le pont.

#### Surcharges

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`supportePaireJeton`](StandardBridgeAdapter.md#supportstokenpair)

#### Source

src/adapters/eth-bridge.ts:105

***

### retirer()

> **retirer**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

Retire des jetons vers la chaîne L1.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à retirer.

• **signer**: `Signer`

Signer utilisé pour signer et envoyer la transaction.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour la transaction de retrait.

#### Hérité de

[`StandardBridgeAdapter`](StandardBridgeAdapter.md).[`retirer`](StandardBridgeAdapter.md#withdraw-2)

#### Source

src/adapters/standard-bridge.ts:274
