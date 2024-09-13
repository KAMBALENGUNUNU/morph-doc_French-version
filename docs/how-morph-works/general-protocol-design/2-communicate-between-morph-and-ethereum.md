---
title: Communication entre Morph et Ethereum
lang: fr-FR
keywords: [morph,ethereum,rollup,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution zk-rollup optimiste décentralisée, sécurisée, rentable et performante. Essayez-le maintenant !
---

Bien que Morph soit une solution Layer 2 construite sur Ethereum, elle reste une blockchain distincte. Ainsi, il est essentiel d'établir un canal de communication entre Morph et Ethereum pour faciliter le transfert fluide d'actifs et de messages. La communication peut se faire dans deux directions : d'Ethereum vers Morph et de Morph vers Ethereum.

## Les bases du pont Morph - Ethereum​

Le transfert d'actifs entre Ethereum et Morph implique le processus suivant :

- **Verrouillage et emballage des actifs** : Pour initier le transfert, un utilisateur doit verrouiller son actif sur le pont inter-couches. Une fois le verrouillage confirmé, Morph frappe un Token Représentatif qui correspond à la valeur de l'actif verrouillé, dans une procédure appelée "dépôt".

- **Réception d'actifs** : Après la frappe, l'utilisateur ou le destinataire recevra l'actif sur Morph, reflétant la valeur de l'actif initialement verrouillé.

- **Processus inverse** : À l'inverse, pour transférer des actifs vers Ethereum, le pont peut débloquer l'actif d'origine sur Ethereum en brûlant le Token Représentatif sur Morph. Cela s'appelle un "retrait".

En outre, l'utilité du pont dépasse les simples transferts d'actifs. Il utilise le même principe pour les transferts de messages, permettant la transmission de données entre les deux couches du réseau.

## Comprendre le Gateway

Le **Gateway** sert de point d'entrée principal pour les utilisateurs souhaitant interagir avec le système de pont dans son ensemble. Bien que le processus de base pour transférer des actifs repose toujours sur la transmission de messages, nous recommandons d'utiliser l'approche Gateway pour des transactions inter-couches efficaces.

Pour répondre aux divers besoins de transfert d'actifs, nous avons conçu plusieurs Gateways distincts tels que l'ETH Gateway, le Gateway ERC20 standard, et d'autres.

Nous avons également mis en place un **Gateway Router** qui appelle différents Gateways en fonction du type d'actifs que vous possédez, facilitant ainsi une interaction transparente avec le contrat Gateway Router.

| Contrat Gateway L1         | Description                                                      |
| ------------------------ | ---------------------------------------------------------------- |
| `L1GatewayRouter`        | Le router pour déposer des ETH et des tokens ERC20.               |
| `L1ETHGateway`           | Le gateway pour déposer des ETH.                                  |
| `L1StandardERC20Gateway` | Le gateway pour les dépôts de tokens ERC20 standards.             |
| `L1CustomERC20Gateway`   | Le gateway pour les dépôts de tokens ERC20 personnalisés.         |
| `L1WETHGateway`          | Le gateway pour les dépôts d'ETH encapsulés (WETH).               |

| Contrat Gateway L2         | Description                                                      |
| ------------------------ | ---------------------------------------------------------------- |
| `L2GatewayRouter`        | Le router pour retirer des ETH et des tokens ERC20.               |
| `L2ETHGateway`           | Le gateway pour retirer des ETH.                                  |
| `L2StandardERC20Gateway` | Le gateway pour les retraits de tokens ERC20 standards.           |
| `L2CustomERC20Gateway`   | Le gateway pour les retraits de tokens ERC20 personnalisés.       |
| `L2WETHGateway`          | Le gateway pour les retraits d'ETH encapsulés (WETH).             |

## Dépôt (Message L1 vers L2)

![Processus de Dépôt](../../../assets/docs/protocol/general/bridge/deposit.png)

### Construire une demande de dépôt via le Gateway

Une demande de pont, qu'il s'agisse d'ETH, ERC20 ou ERC721, est essentiellement un message inter-couches, qui nécessite la construction initiale d'un message.

Généralement, la structure du message reste cohérente, notamment pour les Gateways ETH et ERC20.

L'utilisation d'un token gateway compile un message standard et le relaie au ```CrossDomainMessenger```.

### Transmission du message via le CrossDomainMessenger

Le ```CrossDomainMessenger``` sert de composant central pour la communication inter-couches, avec des contrats correspondants sur Layer 1 et Layer 2.

Pour un dépôt, le messager L1 envoie un message au messager L2, similaire à un appel de contrat sur Layer 1, ce qui signifie que des messages personnalisés peuvent être construits pour diverses interactions inter-couches.

### Exécution du message sur Layer 2

Le message inter-couches est livré au ```L1MessageQueueWithGasPriceOracle```, ce qui déclenche un événement appelé ```QueueTransaction```.

Le Séquenceur surveillera cet événement et inclura une transaction Layer 2 dans son prochain bloc.

### Comment s'assurer que le Séquenceur ne falsifie pas une transaction de dépôt ?

Les séquenceurs pourraient être tentés de forger une transaction de dépôt inexistante, comme frapper une grande quantité de tokens Layer 2 et les transférer à une adresse qu'ils possèdent.

Morph prévient ces risques par deux mesures :

- L'architecture décentralisée des séquenceurs de Morph rend la falsification de transactions très difficile sans contrôler au moins deux tiers des Séquenceurs.

- Le cadre zkEVM optimiste de Morph permet aux challengers de détecter ce comportement malveillant et d'initier des défis pour corriger l'inconduite.

Un exécuteur Layer 2, détenant le message inter-couches, interagit avec le messager L2 pour exécuter le message, ce qui peut inclure le transfert d'ETH L2 ou de tokens ERC20 à leur destinataire.

### Finalisation du message de dépôt

La finalisation du processus de dépôt implique plus que l'exécution de la demande sur Layer 2. Il est possible que l'exécution Layer 2 et sa mise à jour d'état correspondante puissent être annulées en raison de la détection de données incorrectes dans le processus de défi.

Ainsi, une demande de dépôt n'est considérée comme complète que lorsque le lot correspondant à la transaction d'exécution du dépôt est finalisé.

En général, cela suit un flux de travail simple :

- Les transactions d'exécution de dépôt sont compilées en lot et soumises à Layer 1 par les soumetteurs de lots.

- Après la période de défi, les lots valides sont finalisés par des soumissions de lots ultérieures via ```rollup.commitBatch```.

- Pendant la finalisation, le ```L1MessageQueueAndGasPriceOracle``` supprime (pop) le message de dépôt de la file d'attente, marquant ainsi la fin du processus de dépôt.

## Retrait (Message L2 -> L1)

![Processus de Retrait](../../../assets/docs/protocol/general/bridge/withdraw.png)

### Finalisation d'un Retrait

Contrairement aux Dépôts, une demande de retrait doit passer par 2 processus avant son exécution :

1. Prouver qu'une demande de retrait a réellement eu lieu sur la Layer 2 en vérifiant une preuve d'arbre Merkle contre la racine de l'arbre de retrait validée par les séquenceurs.

2. Attendre la fin de la période de contestation et finaliser la racine de l'arbre de retrait, pour éviter que les séquenceurs ne soumettent des données de lot incorrectes, y compris la racine de l'arbre de retrait.

En général, ces deux processus se déroulent simultanément. Une fois la racine de l'arbre de retrait finalisée, les utilisateurs peuvent appeler la méthode ```proveAndRelayMessage``` dans le contrat ```L1CrossDomainMessenger``` pour exécuter le message de retrait.

```solidity
function proveAndRelayMessage(
        address _from,
        address _to,
        uint256 _value,
        uint256 _nonce,
        bytes memory _message,
        bytes32[32] calldata _withdrawalProof,
        bytes32 _withdrawalRoot
    )

```

Cette fonction a deux objectifs principaux :

Vérifier si la racine de l'arbre de retrait associée à ce message a été finalisée via le contrat rollup.
Valider si la demande de retrait a réellement eu lieu en validant la preuve Merkle fournie.
Une fois ces deux processus terminés avec succès, cette méthode exécutera l'action correspondante, comme la libération des ETH de l'utilisateur sur Layer 1 pour une demande de retrait d'ETH standard.

### Comprendre l'Arbre de Retrait

Les actions de retrait impliquent d'interagir avec des actifs/contrats L1 à la suite d'une transaction Layer 2. Par conséquent, il est essentiel de vérifier l'existence d'une transaction Layer 2 déclenchant une demande de retrait, d'une manière vérifiable sur Layer 1.

Pour cela, nous introduisons une structure appelée Arbre de Retrait, qui enregistre chaque transaction de retrait L2 dans un arbre de Merkle. Ainsi, les propriétés de l'arbre de Merkle peuvent être utilisées pour confirmer la survenue d'une demande de retrait.

Le terme Arbre de Retrait fait référence à un Arbre de Merkle Sparse (SMT) en mode ajout-seul, dont les nœuds feuilles capturent les informations sur les actifs transférés hors du réseau. Chaque feuille dans l'Arbre de Retrait, connue sous le nom de feuille de Retrait, appartient à deux catégories : type 0 pour enregistrer des informations d'actif(s) et type 1 pour enregistrer des informations de messagerie.

Une feuille de Retrait est un hash Keccak256 de la structure ABI encodée de manière packée avec un message inter-domaines.

L'Arbre de Retrait est essentiel pour cataloguer les transactions de retrait et vérifier la légitimité des demandes de retrait.

Morph a pré-déployé un contrat d'Arbre de Merkle Simple dédié à la construction de l'arbre de retrait de Layer 2.

Cet arbre intègre trois méthodes :

1. ```getTreeroot``` - Récupère le hash racine actuel de l'arbre.
2. ```appendMessageHash``` - Ajoute un nouveau nœud feuille à l'arbre.
3. ```verifyMerkleProof``` - Vérifie si un nœud feuille existe dans l'arbre, ce qui indique la validité de la demande de pontage qu'il représente.

### Comprendre la Période de Contestation & la Finalisation des Batches

L'architecture zkEVM Optimiste exige que chaque transaction L2 soit soumise à Layer 1 et passe par une période de contestation avant d'être finalisée.

Ce processus est essentiel pour valider l'état de Layer 2 et, finalement, valider l'authenticité de la demande de retrait.

La racine de l'arbre de retrait, cruciale pour la vérification des demandes de retrait, est également soumise par les séquenceurs une fois que la période de contestation, les batches et les états ont été finalisés.

## Erreurs Inter-couches (Pont)
Avec la conception des ponts inter-couches, le message inter-couches pour les dépôts doit être exécuté et mettre à jour ses états Layer 2. L'envoi d'une demande inter-chaînes réussie ne garantit pas son exécution sur L2.

Avant cela, il existe une possibilité que le message inter-couches échoue lors de l'exécution sur Layer 2. Cette section décrit les scénarios potentiels et les solutions pour gérer les messages de dépôt inter-couches échoués.

### Scénarios d'échec Inter-couches (Pont) :

Deux types principaux d'échecs peuvent survenir dans les communications inter-couches (pont) :

Échec de Gaz : Les messages inter-couches envoyés de L1 à L2 peuvent échouer lors de leur exécution sur L2 en raison de limitations dans gasLimit ou la logique du code.

Message Ignoré : Certaines exécutions de données peuvent provoquer des débordements dans les circuits des nœuds L2, entraînant l'omission ou l'ignorance des messages inter-couches.

### Gestion des Échecs Inter-couches (Pont) :

Pour les Échecs de Gaz :

- Lorsque le contrat ```L1CrossDomainMessenger``` sur L1 envoie un message inter-couches, il enregistre le hash correspondant du message mais n'intègre pas le gasLimit dans cet enregistrement. Après l'exécution sur L2, le  ```L2CrossDomainMessenger``` effectue un calcul équivalent, stockant le résultat de l'appel du contrat dans ```mapping(isL1MessageExecuted)```.Cette mesure empêche l'exécution multiple du même message et facilite l'ajustement des paramètres de gasLimit pour rejouer les messages échoués.

- Rejouer le Message : Si gasLimit est insuffisant, provoquant un échec d'exécution sur L2, un nouveau message inter-couches avec un paramètre gasLimit révisé peut être envoyé en appelant  ```L1CrossDomainMessenger.replayMessage```.
Pour les Messages Ignorés :

- Les messages abandonnés en raison de débordements potentiels de circuits sur L2 sont ignorés et non exécutés. Les contrats d'appel inter-couches personnalisés doivent implémenter la méthode
```onDropMessage```pour tenir compte de ces cas.

- Le contrat gateway inclut la méthode onDropMessage, conçue pour rembourser l'initiateur du message inter-couches.

- Appeler  ```L1CrossDomainMessenger.dropMessage``` permet de supprimer le message inter-couches et de déclencher la méthode onDropMessage dans le contrat d'origine, en passant la valeur et le message de la transaction comme msg.value et paramètres de la méthode, respectivement.
