[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / CrossChainMessenger

# Classe : CrossChainMessenger

## Constructeurs

### nouveau CrossChainMessenger()

> **nouveau CrossChainMessenger**(`opts`): [`CrossChainMessenger`](CrossChainMessenger.md)

Crée une nouvelle instance de CrossChainProvider.

#### Paramètres

• **opts**

Options pour le fournisseur.

• **opts.backendURL?**: `string`

backend pour la génération de preuve de retrait.

• **opts.bridges?**: [`BridgeAdapterData`](../interfaces/BridgeAdapterData.md)

Liste optionnelle d'adresses de ponts.

• **opts.contracts?**: [`DeepPartial`](../type-aliases/DeepPartial.md)\<[`OEContractsLike`](../interfaces/OEContractsLike.md)\>

Remplacements optionnels des adresses de contrats.

• **opts.l1ChainId**: [`NumberLike`](../type-aliases/NumberLike.md)

ID de la chaîne pour la chaîne L1.

• **opts.l1SignerOrProvider**: [`SignerOrProviderLike`](../type-aliases/SignerOrProviderLike.md)

Signataire ou Fournisseur pour la chaîne L1, ou une URL JSON-RPC.

• **opts.l2ChainId**: [`NumberLike`](../type-aliases/NumberLike.md)

ID de la chaîne pour la chaîne L2.

• **opts.l2SignerOrProvider**: [`SignerOrProviderLike`](../type-aliases/SignerOrProviderLike.md)

Signataire ou Fournisseur pour la chaîne L2, ou une URL JSON-RPC.

#### Renvoie

[`CrossChainMessenger`](CrossChainMessenger.md)

#### Source

src/cross-chain-messenger.ts:130

## Propriétés

### backendURL

> **backendURL**: `string`

URL du backend pour le serveur de preuve de retrait.

#### Source

src/cross-chain-messenger.ts:76

***

### bridges

> **bridges**: [`BridgeAdapters`](../interfaces/BridgeAdapters.md)

Liste des ponts personnalisés pour le réseau donné.

#### Source

src/cross-chain-messenger.ts:116

***

### contracts

> **contracts**: [`OEContracts`](../interfaces/OEContracts.md)

Objets de contrats attachés à leurs fournisseurs et adresses respectifs.

#### Source

src/cross-chain-messenger.ts:111

***

### estimateGas

> **estimateGas**: `objet`

Objet qui contient les fonctions pour estimer le gaz requis pour une transaction donnée.
Suit le modèle utilisé par ethers.js.

#### approveERC20()

> **approveERC20**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`BigNumber`\>

Estime le gaz nécessaire pour approuver certains tokens à déposer dans la chaîne L2.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du token L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du token à approuver.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Renvoie

`Promise`\<`BigNumber`\>

#### depositERC20()

> **depositERC20**: (`l1Token`, `l2Token`, `amount`, `opts`?) => `Promise`\<`BigNumber`\>

Estime le gaz nécessaire pour déposer des tokens ERC20 dans la chaîne L2.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à déposer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Renvoie

`Promise`\<`BigNumber`\>

#### depositETH()

> **depositETH**: (`amount`, `opts`?) => `Promise`\<`BigNumber`\>

Estime le gaz nécessaire pour déposer de l'ETH dans la chaîne L2.

##### Paramètres

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant d'ETH à déposer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Renvoie

`Promise`\<`BigNumber`\>

#### proveAndRelayMessage()

> **proveAndRelayMessage**: (`message`, `opts`?) => `Promise`\<`BigNumber`\>

Estime le gaz nécessaire pour prouver et relayer un message inter-chaînes. Cela s'applique uniquement aux messages de L2 à L1.

##### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message pour générer la transaction de preuve.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Renvoie

`Promise`\<`BigNumber`\>

#### sendMessage()

> **sendMessage**: (`message`, `opts`?) => `Promise`\<`BigNumber`\>

Estime le gaz nécessaire pour envoyer un message inter-chaînes.

##### Paramètres

• **message**: [`CrossChainMessageRequest`](../interfaces/CrossChainMessageRequest.md)

Message inter-chaînes à envoyer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Renvoie

`Promise`\<`BigNumber`\>

#### retirerERC20()

> **retirerERC20**: (`l1Token`, `l2Token`, `montant`, `opts`?) => `Promise`\<`BigNumber`\>

Estime le gas requis pour retirer des tokens ERC20 vers la chaîne L1.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token sur L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token sur L2.

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à retirer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`BigNumber`\>

#### retirerETH()

> **retirerETH**: (`montant`, `opts`?) => `Promise`\<`BigNumber`\>

Estime le gas requis pour retirer de l'ETH vers la chaîne L1.

##### Paramètres

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant d'ETH à retirer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`BigNumber`\>

#### Source

src/cross-chain-messenger.ts:1600

***

### l1ChainId

> **l1ChainId**: `number`

ID de la chaîne pour le réseau L1.

#### Source

src/cross-chain-messenger.ts:101

***

### l1CrossDomainMessenger

> **l1CrossDomainMessenger**: `Contract`

CrossDomainMessenger connecté à la chaîne L1.

#### Source

src/cross-chain-messenger.ts:91

***

### l1SignerOrProvider

> **l1SignerOrProvider**: `Provider` \| `Signer`

Fournisseur ou signataire connecté à la chaîne L1.

#### Source

src/cross-chain-messenger.ts:81

***

### l2ChainId

> **l2ChainId**: `number`

ID de la chaîne pour le réseau L2.

#### Source

src/cross-chain-messenger.ts:106

***

### l2CrossDomainMessenger

> **l2CrossDomainMessenger**: `Contract`

CrossDomainMessenger connecté à la chaîne L2.

#### Source

src/cross-chain-messenger.ts:96

***

### l2SignerOrProvider

> **l2SignerOrProvider**: `Provider` \| `Signer`

Fournisseur ou signataire connecté à la chaîne L2.

#### Source

src/cross-chain-messenger.ts:86

***

### populateTransaction

> **populateTransaction**: `objet`

Objet qui contient les fonctions générant des transactions à signer par l'utilisateur. Suivant le modèle utilisé par ethers.js.

#### approuverERC20()

> **approuverERC20**: (`l1Token`, `l2Token`, `montant`, `opts`?) => `Promise`\<`TransactionRequest`\>

Génère une transaction pour approuver des tokens à déposer sur la chaîne L2.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token sur L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token sur L2.

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du token à approuver.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retourne

`Promise`\<`TransactionRequest`\>

#### déposerERC20()

> **déposerERC20**: (`l1Token`, `l2Token`, `montant`, `opts`?, `estimerGas`) => `Promise`\<`TransactionRequest`\>

Génère une transaction pour déposer des tokens ERC20 sur la chaîne L2.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token sur L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token sur L2.

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à déposer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### retirerERC20()

> **retirerERC20**: (`l1Token`, `l2Token`, `montant`, `options`?) => `Promise`\<`BigNumber`\>

Estime le gaz requis pour retirer des tokens ERC20 vers la chaîne L1.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L2.

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à retirer.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retours

`Promise`\<`BigNumber`\>

#### retirerETH()

> **retirerETH**: (`montant`, `options`?) => `Promise`\<`BigNumber`\>

Estime le gaz requis pour retirer des ETH vers la chaîne L1.

##### Paramètres

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant de ETH à retirer.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retours

`Promise`\<`BigNumber`\>

#### Source

src/cross-chain-messenger.ts:1600

***

### l1ChainId

> **l1ChainId**: `nombre`

Identifiant de la chaîne L1.

#### Source

src/cross-chain-messenger.ts:101

***

### l1CrossDomainMessenger

> **l1CrossDomainMessenger**: `Contrat`

CrossDomainMessenger connecté à la chaîne L1.

#### Source

src/cross-chain-messenger.ts:91

***

### l1SignerOuProvider

> **l1SignerOuProvider**: `Provider` \| `Signer`

Fournisseur connecté à la chaîne L1.

#### Source

src/cross-chain-messenger.ts:81

***

### l2ChainId

> **l2ChainId**: `nombre`

Identifiant de la chaîne L2.

#### Source

src/cross-chain-messenger.ts:106

***

### l2CrossDomainMessenger

> **l2CrossDomainMessenger**: `Contrat`

CrossDomainMessenger connecté à la chaîne L2.

#### Source

src/cross-chain-messenger.ts:96

***

### l2SignerOuProvider

> **l2SignerOuProvider**: `Provider` \| `Signer`

Fournisseur connecté à la chaîne L2.

#### Source

src/cross-chain-messenger.ts:86

***

### peuplerTransaction

> **peuplerTransaction**: `objet`

Objet qui contient les fonctions générant des transactions à signer par l'utilisateur.
Suit le modèle utilisé par ethers.js.

#### approuverERC20()

> **approuverERC20**: (`l1Token`, `l2Token`, `montant`, `options`?) => `Promise`\<`TransactionRequest`\>

Génère une transaction pour approuver des tokens à déposer dans la chaîne L2.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L2.

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du token à approuver.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retours

`Promise`\<`TransactionRequest`\>

#### déposerERC20()

> **déposerERC20**: (`l1Token`, `l2Token`, `montant`, `options`?, `estimationGaz`) => `Promise`\<`TransactionRequest`\>

Génère une transaction pour déposer des tokens ERC20 dans la chaîne L2.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L2.

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à déposer.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

• **estimationGaz?**: `boolean`= `false`

##### Retours

`Promise`\<`TransactionRequest`\>

#### déposerETH()

> **déposerETH**: (`montant`, `options`?, `estimationGaz`) => `Promise`\<`TransactionRequest`\>

Génère une transaction pour déposer des ETH dans la chaîne L2.

##### Paramètres

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant de ETH à déposer.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

• **estimationGaz?**: `boolean`= `false`

##### Retours

`Promise`\<`TransactionRequest`\>

#### prouverEtRelayerMessage()

> **prouverEtRelayerMessage**: (`message`, `options`?) => `Promise`\<`TransactionRequest`\>

Génère une transaction de preuve et de relais de message qui peut être signée et exécutée. Seulement
applicable pour les messages L2 vers L1.

##### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message pour générer la transaction de preuve.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retours

`Promise`\<`TransactionRequest`\>

#### envoyerMessage()

> **envoyerMessage**: (`message`, `options`?) => `Promise`\<`TransactionRequest`\>

Génère une transaction qui envoie un message cross-chain donné. Cette transaction peut être signée
et exécutée par un signataire.

##### Paramètres

• **message**: [`CrossChainMessageRequest`](../interfaces/CrossChainMessageRequest.md)

Message cross-chain à envoyer.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

##### Retours

`Promise`\<`TransactionRequest`\>

#### retirerERC20()

> **retirerERC20**: (`l1Token`, `l2Token`, `montant`, `options`?, `estimationGaz?`) => `Promise`\<`TransactionRequest`\>

Génère une transaction pour retirer des tokens ERC20 vers la chaîne L1.

##### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L2.

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à retirer.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

• **estimationGaz?**: `boolean`

##### Retours

`Promise`\<`TransactionRequest`\>

#### retirerETH()

> **retirerETH**: (`montant`, `options`?, `estimationGaz?`) => `Promise`\<`TransactionRequest`\>

Génère une transaction pour retirer des ETH vers la chaîne L1.

##### Paramètres

• **montant**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant de ETH à retirer.

• **options?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

• **estimationGaz?**: `boolean`

##### Retours

`Promise`\<`TransactionRequest`\>

#### Source

src/cross-chain-messenger.ts:1304

## Accesseurs

### l1Provider

> `get` **l1Provider**(): `Provider`

Fournisseur connecté à la chaîne L1.

##### Retours

`Provider`

#### Source

src/cross-chain-messenger.ts:193

***

### l1Signer

> `get` **l1Signer**(): `Signer`

Signataire connecté à la chaîne L1.

##### Retours

`Signer`

#### Source

src/cross-chain-messenger.ts:215

***

### l2Provider

> `get` **l2Provider**(): `Provider`

Fournisseur connecté à la chaîne L2.

##### Retours

`Provider`

#### Source

src/cross-chain-messenger.ts:204

***

### l2Signer

> `get` **l2Signer**(): `Signer`

Signataire connecté à la chaîne L2.

#### Retourne

`Signer`

#### Source

src/cross-chain-messenger.ts:226

## Méthodes

### approval()

> **approval**(`l1Token`, `l2Token`, `opts`?): `Promise`\<`BigNumber`\>

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

Montant de jetons approuvés pour les dépôts à partir du compte.

#### Source

src/cross-chain-messenger.ts:1214

***

### approveERC20()

> **approveERC20**(`l1Token`, `l2Token`, `amount`, `opts`?): `Promise`\<`TransactionResponse`\>

Approuve un dépôt sur la chaîne L2.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

L'adresse du jeton L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant du jeton à approuver.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour l'approbation.

#### Source

src/cross-chain-messenger.ts:1233

***

### depositERC20()

> **depositERC20**(`l1Token`, `l2Token`, `amount`, `opts`?): `Promise`\<`TransactionResponse`\>

Dépose des jetons ERC20 dans la chaîne L2.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du jeton L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du jeton L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à déposer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour le dépôt.

#### Source

src/cross-chain-messenger.ts:1256

***

### depositETH()

> **depositETH**(`amount`, `opts`?): `Promise`\<`TransactionResponse`\>

Dépose de l'ETH dans la chaîne L2.

#### Paramètres

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant d'ETH à déposer (en wei).

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour le dépôt.

#### Source

src/cross-chain-messenger.ts:1183

***

### encodeFunctionMessage()

> **encodeFunctionMessage**(`options`): `string`

Encode un message pour le contrat L2CrossDomainMessenger, tel que hashCrossDomainMessagev1.

#### Paramètres

• **options**

• **options.message**: `string`

Le message transmis avec le message cross-chain.

• **options.messageNonce**: `BigNumber`

Le nonce du message cross-chain.

• **options.sender**: `string`

L'expéditeur du message cross-chain.

• **options.target**: `string`

Le destinataire du message cross-chain.

• **options.value**: `BigNumber`

La valeur envoyée avec le message cross-chain.

#### Retourne

`string`

#### Source

src/cross-chain-messenger.ts:972

***

### estimateL2MessageGasLimit()

> **estimateL2MessageGasLimit**(`message`, `opts`?): `Promise`\<`BigNumber`\>

Estime la quantité de gas nécessaire pour exécuter pleinement un message donné sur L2. 
Applicable uniquement aux messages L1 => L2. Vous devez fournir cette limite de gas lors de l'envoi du message à L2.



#### Parametre

• **message**: [`MessageRequestLike`](../type-aliases/MessageRequestLike.md)

Message pour lequel obtenir une estimation de gas.


• **opts?**

Objet d'options.

• **opts.bufferPercent?**: `number`

Pourcentage de gas à ajouter à l'estimation. Par défaut 20%.


• **opts.from?**: `string`

Adresse à utiliser comme expéditeur.


#### Retourne


`Promise`\<`BigNumber`\>

Estimation de la limite de gas sur L2.


#### Source

src/cross-chain-messenger.ts:918

***

### getBackendTreeSyncIndex()

> **getBackendTreeSyncIndex**(): `Promise`\<`number`\>

#### Returns

`Promise`\<`number`\>

#### Source

src/cross-chain-messenger.ts:1122

***

### getBridgeForTokenPair()

> **getBridgeForTokenPair**(`l1Token`, `l2Token`): `Promise`\<[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md)\>

Trouve l'adaptateur de pont approprié pour un couple de jetons L1 - L2. Lève une exception s'il n'existe aucun pont supportant le couple de jetons ou si plus d'un pont supporte le couple de jetons.

#### Parametre

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du jeton L1.


• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du jeton L2.


#### Retourne

`Promise`\<[`IBridgeAdapter`](../interfaces/IBridgeAdapter.md)\>

L'adaptateur de pont approprié pour le couple de jetons donné.


#### Source

src/cross-chain-messenger.ts:378

***

### getCommittedL2BlockNumber()

> **getCommittedL2BlockNumber**(): `Promise`\<`any`\>

#### Retourne


`Promise`\<`any`\>

#### Source

src/cross-chain-messenger.ts:995

***

### getDepositsByAddress()

> **getDepositsByAddress**(`address`, `opts`): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Obtient tous les dépôts pour une adresse donnée.


#### Parametre

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse pour laquelle rechercher des messages.


• **opts**= `{}`

Objet d'options.
• **opts.fromBlock?**: `BlockTag`

Bloc à partir duquel commencer la recherche de messages. Si non fourni, commencera
à partir du premier bloc (bloc #0).

• **opts.toBlock?**: `BlockTag`

Bloc pour arrêter la recherche de messages. Si non fourni, s'arrêtera
au dernier bloc connu ("dernier").

#### Renvoie

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Tous les messages de pont de jetons de dépôt envoyés par l'adresse donnée.

#### Source

src/cross-chain-messenger.ts:424

***

### getFinalizedL2BlockNumber()

> **getFinalizedL2BlockNumber**(): `Promise`\<`any`\>

#### Renvoie

`Promise`\<`any`\>

#### Source

src/cross-chain-messenger.ts:1017

***

### getMessageReceipt()

> **getMessageReceipt**(`message`, `opts`): `Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

Trouve le reçu de la transaction qui a exécuté un message inter-chaîne particulier.

#### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message pour lequel trouver le reçu.

• **opts**= `{}`

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Renvoie

`Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

Reçu CrossChainMessage, incluant le reçu de la transaction qui a relayé le
message donné.

#### Source

src/cross-chain-messenger.ts:757

***

### getMessageStatus()

> **getMessageStatus**(`message`, `opts`): `Promise`\<[`MessageStatus`](../enumerations/MessageStatus.md)\>

Récupère le statut d'un message particulier sous forme d'énumération.

#### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message inter-chaîne pour vérifier le statut.

• **opts**= `{}`

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Renvoie

`Promise`\<[`MessageStatus`](../enumerations/MessageStatus.md)\>

Statut du message.

#### Source

src/cross-chain-messenger.ts:634

***

### getMessagesByTransaction()

> **getMessagesByTransaction**(`transaction`, `opts`): `Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)[]\>

Récupère tous les messages inter-chaîne envoyés dans une transaction donnée.

#### Paramètres

• **transaction**: [`TransactionLike`](../type-aliases/TransactionLike.md)

Hash ou reçu de la transaction pour trouver les messages.

• **opts**= `{}`

Objet d'options.

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

Direction pour chercher des messages. Si non fourni, essaiera de
rechercher automatiquement dans les deux directions, en supposant qu'un hash de transaction n'existera que
sur une seule chaîne. Si le hash existe sur les deux chaînes, cela génèrera une erreur.

#### Renvoie

`Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)[]\>

Tous les messages inter-chaîne envoyés dans la transaction.

#### Source

src/cross-chain-messenger.ts:244

***

### getProvenWithdrawal()

> **getProvenWithdrawal**(`withdrawalHash`): `Promise`\<[`ProvenWithdrawal`](../interfaces/ProvenWithdrawal.md)\>

Interroge le mappage `provenWithdrawals` du contrat L1CrossDomainMessenger pour un ProvenWithdrawal qui correspond au withdrawalHash fourni.

#### Parametre

• **withdrawalHash**: `string`

#### Returne

`Promise`\<[`ProvenWithdrawal`](../interfaces/ProvenWithdrawal.md)\>

Un objet ProvenWithdrawal

#### Source

src/cross-chain-messenger.ts:957

***

### getWithdrawMessageProof()

> **getWithdrawMessageProof**(`message`): `Promise`\<[`WithdrawMessageProof`](../interfaces/WithdrawMessageProof.md)\>

Génère la preuve nécessaire pour finaliser un message de L2 à L1.

#### Parameters

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message pour lequel générer une preuve.

#### Returne

`Promise`\<[`WithdrawMessageProof`](../interfaces/WithdrawMessageProof.md)\>

Preuve qui peut être utilisée pour finaliser le message.

#### Source

src/cross-chain-messenger.ts:1042

***

### getWithdrawalsByAddress()

> **getWithdrawalsByAddress**(`address`, `opts`): `Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Récupère tous les retraits pour une adresse donnée.

#### Paramètres

• **address**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse pour rechercher les messages.

• **opts**= `{}`

Objet d'options.

• **opts.fromBlock?**: `BlockTag`

Bloc à partir duquel commencer la recherche de messages. Si non fourni, commencera à partir du premier bloc (bloc #0).

• **opts.toBlock?**: `BlockTag`

Bloc où arrêter la recherche de messages. Si non fourni, s'arrêtera au dernier bloc connu ("latest").

#### Returne

`Promise`\<[`TokenBridgeMessage`](../interfaces/TokenBridgeMessage.md)[]\>

Tous les messages de pont de jetons de retrait envoyés par l'adresse donnée.

#### Source

src/cross-chain-messenger.ts:458

***

### proveAndRelayMessage()

> **proveAndRelayMessage**(`message`, `opts`?): `Promise`\<`TransactionResponse`\>

Prouve et relaye un message inter-chaînes envoyé de L2 à L1. Applicable uniquement aux messages L2 vers L1.

#### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message à finaliser.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour la finalisation du message.

#### Source

src/cross-chain-messenger.ts:1163

***

### sendMessage()

> **sendMessage**(`message`, `opts`?): `Promise`\<`TransactionResponse`\>

Envoie un message inter-chaînes donné. La destination du message dépend de la direction du message lui-même.

#### Paramètres

• **message**: [`CrossChainMessageRequest`](../interfaces/CrossChainMessageRequest.md)

Message inter-chaînes à envoyer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Retourne

`Promise`\<`TransactionResponse`\>

Réponse de la transaction pour l'envoi du message.

#### Source

src/cross-chain-messenger.ts:1143

***

### toCrossChainMessage()

> **toCrossChainMessage**(`message`, `opts`?): `Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)\>

Résout un MessageLike en un objet CrossChainMessage.
Contrairement aux autres fonctions de coercition, cette fonction est état et nécessite de faire des requêtes supplémentaires. Pour l’instant, je vais garder cette fonction ici, mais nous pourrions envisager de mettre une fonction similaire dans utils/coercion.ts si les gens veulent l'utiliser sans avoir à créer un objet CrossChainProvider entier.

#### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

MessageLike à résoudre en un CrossChainMessage.

• **opts?**

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Retourne

`Promise`\<[`CrossChainMessage`](../interfaces/CrossChainMessage.md)\>

Message contraint en un CrossChainMessage.

#### Source

src/cross-chain-messenger.ts:491

***

### toLowLevelMessage()

> **toLowLevelMessage**(`message`, `opts`?): `Promise`\<[`LowLevelMessage`](../type-aliases/LowLevelMessage.md)\>

Transforme un message CrossChainMessenger en sa représentation de bas niveau à l'intérieur du contrat L2ToL1MessagePasser sur L2.

#### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message à transformer.

• **opts?**

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

#### Returne

`Promise`\<[`LowLevelMessage`](../type-aliases/LowLevelMessage.md)\>

Message transformé.

#### Source

src/cross-chain-messenger.ts:326

***

### waitBatchFinalize()

> **waitBatchFinalize**(`transactionHash`): `Promise`\<`void`\>

#### Paramètres

• **transactionHash**: `string`

#### Returne

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:600

***

### waitForMessageReceipt()

> **waitForMessageReceipt**(`message`, `opts`): `Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

Attend qu'un message soit exécuté et retourne le reçu de la transaction qui a exécuté le message donné.

#### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message à attendre.

• **opts**= `{}`

Options à passer à la fonction d'attente.

• **opts.confirmations?**: `number`

Nombre de confirmations de transaction à attendre avant de retourner.

• **opts.pollIntervalMs?**: `number`

Nombre de millisecondes à attendre entre les vérifications du reçu.

• **opts.timeoutMs?**: `number`

Millisecondes à attendre avant d'arriver à expiration.

#### Returne

`Promise`\<[`MessageReceipt`](../interfaces/MessageReceipt.md)\>

Reçu de CrossChainMessage, y compris le reçu de la transaction qui a relayé le message donné.


#### Source

src/cross-chain-messenger.ts:802

***

### waitForMessageStatus()

> **waitForMessageStatus**(`message`, `status`, `opts`): `Promise`\<`void`\>

Attend jusqu'à ce que le statut d'un message donné change au statut attendu. Notez que si le statut du message donné change vers un statut qui implique le statut attendu, cela retournera quand même. Si le statut du message change vers un statut qui exclut le statut attendu, cela déclenchera une erreur.


#### Paramètres

• **message**: [`MessageLike`](../type-aliases/MessageLike.md)

Message à attendre.

• **status**: [`MessageStatus`](../enumerations/MessageStatus.md)

Statut attendu du message.

• **opts**= `{}`

Options à passer à la fonction d'attente.

• **opts.direction?**: [`MessageDirection`](../enumerations/MessageDirection.md)

• **opts.pollIntervalMs?**: `number`

Nombre de millisecondes à attendre lors des vérifications.

• **opts.timeoutMs?**: `number`

Millisecondes à attendre avant d'arriver à expiration.

#### Retourne

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:840

***

### waitRollupSuccess()

> **waitRollupSuccess**(`transactionHash`): `Promise`\<`void`\>

#### Paramètres

• **transactionHash**: `string`

#### Returne

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:552

***

### waitSyncSuccess()

> **waitSyncSuccess**(`transactionHash`): `Promise`\<`void`\>

#### Paramètres

• **transactionHash**: `string`

#### Returne

`Promise`\<`void`\>

#### Source

src/cross-chain-messenger.ts:576

***

### withdrawERC20()

> **withdrawERC20**(`l1Token`, `l2Token`, `amount`, `opts`?): `Promise`\<`TransactionResponse`\>

Retire des tokens ERC20 vers la chaîne L1.

#### Paramètres

• **l1Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L1.

• **l2Token**: [`AddressLike`](../type-aliases/AddressLike.md)

Adresse du token L2.

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant à retirer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Returne

`Promise`\<`TransactionResponse`\>

Réponse de transaction pour la transaction de retrait.

#### Source

src/cross-chain-messenger.ts:1282

***

### withdrawETH()

> **withdrawETH**(`amount`, `opts`?): `Promise`\<`TransactionResponse`\>

Retire de l'ETH vers la chaîne L1.

#### Paramètres

• **amount**: [`NumberLike`](../type-aliases/NumberLike.md)

Montant d'ETH à retirer.

• **opts?**: [`IActionOptions`](../interfaces/IActionOptions.md)

Options supplémentaires.

#### Returne

`Promise`\<`TransactionResponse`\>

Réponse de transaction pour la transaction de retrait.

#### Source

src/cross-chain-messenger.ts:1198
