[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / CrossChainMessage

# Interface : CrossChainMessage

Décrit un message qui est envoyé entre L1 et L2. La direction détermine d'où le message a été envoyé et où il est envoyé.

## Étend

- [`CoreCrossChainMessage`](CoreCrossChainMessage.md)

## Propriétés

### blockNumber

> **blockNumber** : `number`

#### Source

src/interfaces/types.ts:255

***

### direction

> **direction** : [`MessageDirection`](../enumerations/MessageDirection.md)

#### Source

src/interfaces/types.ts:253

***

### logIndex

> **logIndex** : `number`

#### Source

src/interfaces/types.ts:254

***

### message

> **message** : `string`

#### Hérité de

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`message`](CoreCrossChainMessage.md#message)

#### Source

src/interfaces/types.ts:242

***

### messageNonce

> **messageNonce** : `BigNumber`

#### Hérité de

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`messageNonce`](CoreCrossChainMessage.md#messagenonce)

#### Source

src/interfaces/types.ts:243

***

### minGasLimit

> **minGasLimit** : `BigNumber`

#### Hérité de

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`minGasLimit`](CoreCrossChainMessage.md#mingaslimit)

#### Source

src/interfaces/types.ts:245

***

### sender

> **sender** : `string`

#### Hérité de

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`sender`](CoreCrossChainMessage.md#sender)

#### Source

src/interfaces/types.ts:240

***

### target

> **target** : `string`

#### Hérité de

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`target`](CoreCrossChainMessage.md#target)

#### Source

src/interfaces/types.ts:241

***

### transactionHash

> **transactionHash** : `string`

#### Source

src/interfaces/types.ts:256

***

### value

> **value** : `BigNumber`

#### Hérité de

[`CoreCrossChainMessage`](CoreCrossChainMessage.md).[`value`](CoreCrossChainMessage.md#value)

#### Source

src/interfaces/types.ts:244
