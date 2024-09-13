[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / estimateL2GasCost

# Fonction : estimateL2GasCost()

> **estimateL2GasCost**(`l2Provider`, `tx`) : `Promise`\<`BigNumber`\>

Estime le coût en gaz L2 pour une transaction L2 donnée en wei.

## Paramètres

• **l2Provider** : [`ProviderLike`](../type-aliases/ProviderLike.md)

Fournisseur L2 pour interroger l'utilisation du gaz.

• **tx** : `TransactionRequest`

Transaction pour laquelle estimer le coût en gaz L2.

## Renvoie

`Promise`\<`BigNumber`\>

Coût en gaz L2 estimé.

## Source

src/l2-provider.ts:119
