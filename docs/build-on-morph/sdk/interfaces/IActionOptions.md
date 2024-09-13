[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / IActionOptions

# Interface : IActionOptions

## Param

Signataire optionnel à utiliser pour envoyer la transaction.

## Param

Adresse optionnelle pour recevoir les fonds sur la chaîne. Par défaut, c'est l'expéditeur.

## Param

Direction dans laquelle rechercher des messages. Si non fourni, tentera de
  * rechercher automatiquement dans les deux directions en supposant qu'un hachage de transaction n'existera que
  * sur une seule chaîne. Si le hachage existe sur les deux chaînes, cela lancera une erreur.

## Param

Remplacements de transaction optionnels.

## Propriétés

### direction?

> `optionnel` **direction** : [`MessageDirection`](../enumerations/MessageDirection.md)

#### Source

src/interfaces/types.ts:412

***

### from?

> `optionnel` **from** : `string`

#### Source

src/interfaces/types.ts:410

***

### overrides?

> `optionnel` **overrides** : `object` & `CallOverrides`

#### Déclaration de type

##### gatewayAddress?

> `optionnel` **gatewayAddress** : `string`

##### gatewayName?

> `optionnel` **gatewayName** : `string`

#### Source

src/interfaces/types.ts:413

***

### recipient?

> `optionnel` **recipient** : [`AddressLike`](../type-aliases/AddressLike.md)

#### Source

src/interfaces/types.ts:411

***

### signer?

> `optionnel` **signer** : `Signer`

#### Source

src/interfaces/types.ts:409
