[**@morph-l2/sdk**](../globals.md) • **Docs**

***

[@morph-l2/sdk](../globals.md) / getAllOEContracts

# Fonction : getAllOEContracts()

> **getAllOEContracts**(`l2ChainId`, `opts`) : [`OEContracts`](../interfaces/OEContracts.md)

Se connecte automatiquement à toutes les adresses de contrat, à la fois L1 et L2, pour le L2 chain ID donné. L'utilisateur peut fournir des remplacements d'adresses de contrat personnalisés pour les contrats L1 ou L2. Si le L2 chain ID donné n'est pas connu, l'utilisateur DOIT fournir des adresses de contrat personnalisées pour TOUS les contrats L1 ou cette fonction générera une erreur.

## Paramètres

• **l2ChainId** : `number`

Chain ID pour le réseau L2.

• **opts**= `{}`

Options supplémentaires pour se connecter aux contrats.

• **opts.l1SignerOrProvider?** : `Provider` \| `Signer`

• **opts.l2SignerOrProvider?** : `Provider` \| `Signer`

• **opts.overrides?** : [`DeepPartial`](../type-aliases/DeepPartial.md)\<[`OEContractsLike`](../interfaces/OEContractsLike.md)\>

Remplacements d'adresses de contrat personnalisés pour les contrats L1 ou L2.

## Renvoie

[`OEContracts`](../interfaces/OEContracts.md)

Un objet contenant des objets ethers.Contract connectés aux adresses appropriées sur L1 et L2.

## Source

src/utils/contracts.ts:88
