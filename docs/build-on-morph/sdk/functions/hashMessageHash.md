[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / hashMessageHash

# Fonction : hashMessageHash()

> **hashMessageHash**(`messageHash`) : `string`

Utilitaire pour hacher un hachage de message. Cela calcule l'emplacement de stockage
où le hachage de message sera stocké dans l'état. HashZero est utilisé
car le premier mappage dans le contrat est utilisé.

## Paramètres

• **messageHash** : `string`

Hachage de message à hacher.

## Retourne

`string`

Hachage du hachage de message donné.

## Source

src/utils/message-utils.ts:24
