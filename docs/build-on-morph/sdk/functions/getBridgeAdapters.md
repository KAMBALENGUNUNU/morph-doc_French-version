[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / getBridgeAdapters

# Fonction : getBridgeAdapters()

> **getBridgeAdapters**(l2ChainId, messenger, opts?) : [BridgeAdapters](../interfaces/BridgeAdapters.md)

Obtient une série d'adaptateurs de pont pour l'ID de chaîne L2 donné.

## Paramètres

• **l2ChainId** : nombre

ID de chaîne pour le réseau L2.

• **messenger** : [CrossChainMessenger](../classes/CrossChainMessenger.md)

Messager inter-chaînes pour se connecter aux adaptateurs de pont.

• **opts ?**

Options supplémentaires pour se connecter aux ponts personnalisés.

• **opts.contracts ?** : [DeepPartial](../type-aliases/DeepPartial.md)\<[OEContractsLike](../interfaces/OEContractsLike.md)\>

• **opts.overrides ?** : [BridgeAdapterData](../interfaces/BridgeAdapterData.md)

Adaptateurs de pont personnalisés.

## Retourne

[BridgeAdapters](../interfaces/BridgeAdapters.md)

Un objet contenant tous les adaptateurs de pont.

## Source

src/utils/contracts.ts:142
