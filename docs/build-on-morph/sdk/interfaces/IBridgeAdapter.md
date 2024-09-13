[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / IBridgeAdapter

# Interface : IBridgeAdapter

Représente un adaptateur pour un pont de jetons L1 - L2. Chaque pont personnalisé a actuellement besoin de son propre
adaptateur car l'interface du pont n'est pas standardisée. Cela peut changer à l'avenir.

## Propriétés

### estimateGas

> **estimateGas** : `object`

Objet qui contient les fonctions qui estiment le gaz requis pour une transaction donnée.
Suit le modèle utilisé par ethers.js.

#### approve()

Estime le gaz requis pour approuver des jetons à déposer dans la chaîne L2.

##### Paramètres

• **l1Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount** : [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à approuver.

• **opts?** : [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`BigNumber`\>

Estimation du gaz pour la transaction.

#### deposit()

Estime le gaz requis pour déposer des jetons dans la chaîne L2.

##### Paramètres

• **l1Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount** : [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à déposer.

• **opts?** : [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`BigNumber`\>

Estimation du gaz pour la transaction.

#### withdraw()

Estime le gaz requis pour retirer des jetons vers la chaîne L1.

##### Paramètres

• **l1Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount** : [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à retirer.

• **opts?** : [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`BigNumber`\>

Estimation du gaz pour la transaction.

#### Source

src/interfaces/bridge-adapter.ts:221

***

### l1Bridge

> **l1Bridge** : `Contract`

Contrat de pont L1.

#### Source

src/interfaces/bridge-adapter.ts:38

***

### l2Bridge

> **l2Bridge** : `Contract`

Contrat de pont L2.

#### Source

src/interfaces/bridge-adapter.ts:43

***

### messenger

> **messenger** : [`CrossChainMessenger`](../classes/CrossChainMessenger.md)

Fournisseur utilisé pour faire des requêtes liées aux interactions inter-chaînes.

#### Source

src/interfaces/bridge-adapter.ts:33

***

### populateTransaction

> **populateTransaction** : `object`

Objet qui contient les fonctions qui génèrent des transactions à signer par l'utilisateur.
Suit le modèle utilisé par ethers.js.

#### approve()

Génère une transaction pour approuver des jetons à déposer dans la chaîne L2.

##### Paramètres

• **l1Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount** : [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à approuver.

• **opts?** : [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`TransactionRequest`\>

Transaction qui peut être signée et exécutée pour déposer les jetons.

#### deposit()

Génère une transaction pour déposer des jetons dans la chaîne L2.

##### Paramètres

• **l1Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount** : [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à déposer.

• **opts?** : [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`TransactionRequest`\>

Transaction qui peut être signée et exécutée pour déposer les jetons.

#### withdraw()

Génère une transaction pour retirer des jetons vers la chaîne L1.

##### Paramètres

• **l1Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token** : [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount** : [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à retirer.

• **opts?** : [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`TransactionRequest`\>

Transaction qui peut être signée et exécutée pour retirer les jetons.

#### Source

src/interfaces/bridge-adapter.ts:167

## Méthodes

### approval()

> **approval**(`l1Token`, `l2Token`, `opts`?) : `Promise`\<`BigNumber`\>

Interroge le montant d'approbation du compte pour un jeton L1 donné.
#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L2.

• **opts?**: [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`BigNumber`\>

Montant de tokens approuvés pour les dépôts depuis le compte.

#### Source

src/interfaces/bridge-adapter.ts:103

***

### approve()

> **approve**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

Approuve un dépôt dans la chaîne L2.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du token à approuver.

• **signer**: `Signer`

Signer utilisé pour signer et envoyer la transaction.

• **opts?**: [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour l'opération d'approbation.

#### Source

src/interfaces/bridge-adapter.ts:119

***

### deposit()

> **deposit**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

Dépose des tokens dans la chaîne L2.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du token à déposer.

• **signer**: `Signer`

Signer utilisé pour signer et envoyer la transaction.

• **opts?**: [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour l'opération de dépôt.

#### Source

src/interfaces/bridge-adapter.ts:137

***

### getDepositsByAddress()

> **getDepositsByAddress**(`address`, `opts`?): `Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

Obtient tous les dépôts pour une adresse donnée.

#### Paramètres

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse à partir de laquelle chercher les messages.

• **opts?**

Objet d'options.

• **opts.fromBlock?**: `BlockTag`

Bloc à partir duquel commencer la recherche de messages. S'il n'est pas fourni, commencera
à partir du premier bloc (bloc #0).

• **opts.toBlock?**: `BlockTag`

Bloc à partir duquel arrêter la recherche de messages. S'il n'est pas fourni, s'arrêtera au
dernier bloc connu ("dernier").

#### Retourne

`Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

Tous les messages de dépôt envoyés par l'adresse donnée.

#### Source

src/interfaces/bridge-adapter.ts:56

***

### getWithdrawalsByAddress()

> **getWithdrawalsByAddress**(`address`, `opts`?): `Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

Obtient tous les retraits pour une adresse donnée.

#### Paramètres

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse à partir de laquelle chercher les messages.

• **opts?**

Objet d'options.

• **opts.fromBlock?**: `BlockTag`

Bloc à partir duquel commencer la recherche de messages. S'il n'est pas fourni, commencera
à partir du premier bloc (bloc #0).

• **opts.toBlock?**: `BlockTag`

Bloc à partir duquel arrêter la recherche de messages. S'il n'est pas fourni, s'arrêtera au
dernier bloc connu ("dernier").

#### Retourne

`Promise`\<[`TokenBridgeMessage`](TokenBridgeMessage.md)[]\>

Tous les messages de retrait envoyés par l'adresse donnée.

#### Source

src/interfaces/bridge-adapter.ts:75

***

### supportsTokenPair()

> **supportsTokenPair**(`l1Token`, `l2Token`): `Promise`\<`boolean`\>

Vérifie si la paire de tokens donnée est supportée par le pont.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L2.

#### Retourne

`Promise`\<`boolean`\>

Si la paire de tokens donnée est supportée par le pont.

#### Source

src/interfaces/bridge-adapter.ts:90

***

### withdraw()

> **withdraw**(`l1Token`, `l2Token`, `amount`, `signer`, `opts`?): `Promise`\<`TransactionResponse`\>

Retire des tokens vers la chaîne L1.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du token à retirer.

• **signer**: `Signer`

Signer utilisé pour signer et envoyer la transaction.

• **opts?**: [`IActionOptions`](IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour l'opération de retrait.

#### Source

src/interfaces/bridge-adapter.ts:155
