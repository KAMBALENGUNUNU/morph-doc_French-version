[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / omit

# Fonction : omit()

> **omit**\<`T`, `K`\>(`obj`, ...`keys`) : `Omit`\<`T`, `K`\>

Renvoie une copie de l'objet donné ( ...obj ) avec les clés données omises.

## Paramètres de type

• **T** *extends* `object`

• **K** *extends* `string` \| `number` \| `symbol`

## Paramètres

• **obj** : `T`

Objet à renvoyer avec les clés omises.

• ...**keys** : `K`[]

Clés à omettre de l'objet renvoyé.

## Retourne

`Omit`\<`T`, `K`\>

Une copie de l'objet donné avec les clés omises.

## Source

src/utils/misc-utils.ts:11
