[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / StandardBridgeAdapter

# Classe : StandardBridgeAdapter

Adaptateur de pont pour tout pont de jetons qui utilise l'interface standard de pont de jetons.

## Étendu par

- [`ETHBridgeAdapter`](ETHBridgeAdapter.md)

## Implémente

- [`IBridgeAdapter`](../interfaces/IBridgeAdapter.md)

## Constructeurs

### new StandardBridgeAdapter()

> **new StandardBridgeAdapter**(`opts`): [`StandardBridgeAdapter`](StandardBridgeAdapter.md)

Crée une instance de StandardBridgeAdapter.

#### Paramètres

• **opts**

Options pour l'adaptateur.

• **opts.l1Bridge**: [`AddressLike`](../type-aliases/AddressLike.md)

Contrat de pont L1.

• **opts.l2Bridge**: [`AddressLike`](../type-aliases/AddressLike.md)

Contrat de pont L2.

• **opts.messenger**: [`CrossChainMessenger`](CrossChainMessenger.md)

Fournisseur utilisé pour effectuer des requêtes liées aux interactions inter-chaînes.

#### Retourne

[`StandardBridgeAdapter`](StandardBridgeAdapter.md)

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

##### Retourne

`Promise`\<`BigNumber`\>

#### Implémentation de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`estimateGas`](../interfaces/IBridgeAdapter.md#estimategas)

#### Source

src/adapters/standard-bridge.ts:405

***

### l1Bridge

> **l1Bridge**: `Contract`

Contrat de pont L1.

#### Implémentation de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`l1Bridge`](../interfaces/IBridgeAdapter.md#l1bridge)

#### Source

src/adapters/standard-bridge.ts:41

***

### l2Bridge

> **l2Bridge**: `Contract`

Contrat de pont L2.

#### Implémentation de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`l2Bridge`](../interfaces/IBridgeAdapter.md#l2bridge)

#### Source

src/adapters/standard-bridge.ts:42

***

### messenger

> **messenger**: [`CrossChainMessenger`](CrossChainMessenger.md)

Fournisseur utilisé pour effectuer des requêtes liées aux interactions inter-chaînes.

#### Implémentation de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`messenger`](../interfaces/IBridgeAdapter.md#messenger)

#### Source

src/adapters/standard-bridge.ts:40

***

### populateTransaction

> **populateTransaction**: `object`

Objet qui contient les fonctions qui génèrent des transactions à signer par l'utilisateur.
Suit le modèle utilisé par ethers.js.

#### approve()

> **approve**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`TransactionRequest`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Retourne

`Promise`\<`TransactionRequest`\>

#### deposit()

> **deposit**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`TransactionRequest`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Retourne

`Promise`\<`TransactionRequest`\>

#### withdraw()

> **withdraw**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`TransactionRequest`\>

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

##### Retourne

`Promise`\<`TransactionRequest`\>

#### Implémentation de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`populateTransaction`](../interfaces/IBridgeAdapter.md#populatetransaction)

#### Source

src/adapters/standard-bridge.ts:286

## Méthodes

### approval()

> **approval**(`l1Token`, `l2Token`, `opts`): `Promise`\<`BigNumber`\>

Interroge le montant d'approbation du compte pour un jeton L1 donné.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **opts**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`BigNumber`\>

Montant des jetons approuvés pour les dépôts depuis le compte.

#### Mise en œuvre de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`approval`](../interfaces/IBridgeAdapter.md#approval)

#### Source

src/adapters/standard-bridge.ts:209

***

### approve()

> **approve**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

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

#### Mise en œuvre de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`approve`](../interfaces/IBridgeAdapter.md#approve-2)

#### Source

src/adapters/standard-bridge.ts:250

***

### deposit()

> **deposit**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

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

#### Mise en œuvre de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`deposit`](../interfaces/IBridgeAdapter.md#deposit-2)

#### Source

src/adapters/standard-bridge.ts:262

***

### getDepositsByAddress()

> **getDepositsByAddress**(`address`, `opts`?): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Obtient tous les dépôts pour une adresse donnée.

#### Paramètres

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse à rechercher pour les messages.

• **opts?**

Objet d'options.

• **opts.fromBlock?**: `BlockTag`

• **opts.toBlock?**: `BlockTag`

#### Retourne

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Tous les messages de pont de jetons de dépôt envoyés par l'adresse donnée.

#### Mise en œuvre de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`getDepositsByAddress`](../interfaces/IBridgeAdapter.md#getdepositsbyaddress)

#### Source

src/adapters/standard-bridge.ts:75

***

### getWithdrawalsByAddress()

> **getWithdrawalsByAddress**(`address`, `opts`?): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Obtient tous les retraits pour une adresse donnée.

#### Paramètres

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse à rechercher pour les messages.

• **opts?**

Objet d'options.

• **opts.fromBlock?**: `BlockTag`

• **opts.toBlock?**: `BlockTag`

#### Retourne

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Tous les messages de pont de jetons de retrait envoyés par l'adresse donnée.

#### Mise en œuvre de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`getWithdrawalsByAddress`](../interfaces/IBridgeAdapter.md#getwithdrawalsbyaddress)

#### Source

src/adapters/standard-bridge.ts:122

***

### supportsTokenPair()

> **supportsTokenPair**(`l1Token`, `l2Token`): `Promise`\<`boolean`\>

Vérifie si la paire de jetons donnée est supportée par le pont.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

#### Retourne

`Promise`\<`boolean`\>

Si la paire de jetons donnée est supportée par le pont.

#### Mise en œuvre de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`supportsTokenPair`](../interfaces/IBridgeAdapter.md#supportstokenpair)

#### Source

src/adapters/standard-bridge.ts:165

***

### withdraw()

> **withdraw**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

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

#### Mise en œuvre de

[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md).[`withdraw`](../interfaces/IBridgeAdapter.md#withdraw-2)

#### Source

src/adapters/standard-bridge.ts:274
