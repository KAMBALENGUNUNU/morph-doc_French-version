[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / estimateL1GasCost

# Fonction : estimateL1GasCost()

> **estimateL1GasCost**(`l2Provider`, `tx`) : `Promise`\<`BigNumber`\>

Estime le coût en gaz L1 pour une transaction L2 donnée en wei.

## Paramètres

• **l2Provider** : [`ProviderLike`](../type-aliases/ProviderLike.md)

Fournisseur L2 pour interroger l'utilisation du gaz.

• **tx** : `TransactionRequest`

Transaction pour laquelle estimer le coût en gaz L1.

## Renvoie

`Promise`\<`BigNumber`\>

Coût en gaz L1 estimé.

## Source

src/l2-provider.ts:95
