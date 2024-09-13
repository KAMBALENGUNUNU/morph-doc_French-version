[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / toSignerOrProvider

# Fonction : toSignerOrProvider()

> **toSignerOrProvider**(`signerOrProvider`) : `Provider` \| `Signer`

Convertit un SignerOrProviderLike en un Signer ou un Provider. On suppose que si l'entrée est une chaîne, alors c'est une URL JSON-RPC.

## Paramètres

• **signerOrProvider** : [`SignerOrProviderLike`](../type-aliases/SignerOrProviderLike.md)

SignerOrProviderLike à transformer en Signer ou Provider.

## Retourne

`Provider` \| `Signer`

Entrée sous forme de Signer ou Provider.

## Source

src/utils/coercion.ts:25
