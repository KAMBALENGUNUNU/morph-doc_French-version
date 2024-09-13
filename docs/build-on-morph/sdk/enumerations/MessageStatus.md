[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / MessageStatus

# Énumération : MessageStatus

Énumération décrivant le statut d'un message.

## Membres de l'Énumération

### FAILED\_L1\_TO\_L2\_MESSAGE

> **FAILED\_L1\_TO\_L2\_MESSAGE** : `1`

Le message est un message de L1 à L2 et la transaction pour exécuter le message a échoué.
Lorsque ce statut est retourné, vous devez renvoyer le message de L1 à L2, probablement avec une
limite de gaz plus élevée.

#### Source

src/interfaces/types.ts:186

***

### IN\_CHALLENGE\_PERIOD

> **IN\_CHALLENGE\_PERIOD** : `5`

Le message est un message L2 à L1 prouvé et est en période de contestation.

#### Source

src/interfaces/types.ts:206

***

### READY\_FOR\_RELAY

> **READY\_FOR\_RELAY** : `6`

Le message est prêt à être relayé.

#### Source

src/interfaces/types.ts:211

***

### READY\_TO\_PROVE

> **READY\_TO\_PROVE** : `4`

Le message est prêt à être prouvé sur L1 pour initier la période de contestation.

#### Source

src/interfaces/types.ts:201

***

### RELAYED

> **RELAYED** : `7`

Le message a été relayé.

#### Source

src/interfaces/types.ts:216

***

### UNCONFIRMED\_L1\_TO\_L2\_MESSAGE

> **UNCONFIRMED\_L1\_TO\_L2\_MESSAGE** : `0`

Le message est un message de L1 à L2 et n'a pas été traité par le L2.

#### Source

src/interfaces/types.ts:179

***

### WITHDRAWAL\_HASH\_NOT\_SYNC

> **WITHDRAWAL\_HASH\_NOT\_SYNC** : `3`

Le message est un message L2 à L1 et le hachage de retrait n'a pas encore été publié au backend.

#### Source

src/interfaces/types.ts:196

***

### WITHDRAWAL\_ROOT\_NOT\_PUBLISHED

> **WITHDRAWAL\_ROOT\_NOT\_PUBLISHED** : `2`

Le message est un message L2 à L1 et la racine de retrait n'a pas encore été publiée.

#### Source

src/interfaces/types.ts:191
