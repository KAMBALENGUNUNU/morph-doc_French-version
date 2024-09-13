---
title: La Technologie Derrière Morph
lang: fr-FR
keywords: [morph,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution optimistic zk-rollup sécurisée, décentralisée et performante. Essayez-le maintenant !
---

## Réseau de Séquenceurs Décentralisé

Le Réseau de Séquenceurs Décentralisé de Morph est conçu pour améliorer la sécurité et la fiabilité de la blockchain. Contrairement aux solutions Layer 2 traditionnelles qui reposent sur un séquenceur centralisé, Morph utilise un réseau de séquenceurs décentralisés. Cette configuration garantit qu'aucune entité unique n'a le contrôle sur le processus de séquençage des transactions, éliminant ainsi le risque de point de défaillance unique. Si un séquenceur échoue ou agit de manière malveillante, les autres peuvent continuer à traiter les transactions, maintenant l'intégrité et la disponibilité du système. Cette décentralisation empêche également la censure des transactions et garantit qu'aucune entité ne peut monopoliser la Valeur Extractible par les Mineurs (MEV), créant un environnement plus équitable pour tous les utilisateurs.

Cette approche collaborative augmente non seulement la sécurité, mais améliore également l'efficacité et la fiabilité du système de traitement des transactions, faisant de Morph une solution Layer 2 robuste et résiliente.

![Réseau de Séquenceurs](../../assets/docs/about/overview/seq1.png)

Visitez le [Réseau de Séquenceurs Décentralisé de Morph](../how-morph-works/decentralized-sequencers/1-morph-decentralized-sequencer-network.md) pour un article plus complet.

## Intégration Optimistic zkEVM

Les rollups Optimistic et Zéro-Connaissance (ZK) sont deux approches distinctes pour l'évolutivité des transactions blockchain sur Layer 2. Les rollups optimistes supposent simplement que toutes les transactions sont valides lors de la soumission d'un lot pour règlement sur Ethereum. Cependant, la validité de toute transaction peut être contestée par des entités appelées "challengers", en soumettant une preuve d'activité frauduleuse. Si la preuve de fraude est réussie, la transaction incorrecte est rejetée, garantissant la sécurité mais au prix de quelques retards potentiels et de frais de gaz élevés associés au processus de contestation.

Les rollups ZK, quant à eux, utilisent des preuves cryptographiques pour vérifier la validité des transactions avant qu'elles ne soient soumises pour règlement. Tous les lots ont leur propre preuve ZK, permettant une vérification rapide sur la chaîne principale sans avoir besoin de revoir toutes les données associées à chaque transaction (d'où "zero-knowledge"). Cela offre une finalité immédiate avec une sécurité accrue, mais la génération de ces preuves est coûteuse et nécessite beaucoup de calculs.

Le rollup hybride de Morph combine le meilleur de ces deux approches. Au départ, le système fonctionne de manière optimiste, supposant que les transactions sont valides pour permettre un traitement rapide et des coûts bas. Lorsqu'une transaction est contestée pendant la fenêtre de contestation de Morph, c'est le séquenceur qui doit produire une preuve ZK pour valider la transaction. Nous appelons cette approche Preuve de Validité Réactive (RVP). Elle comporte les améliorations suivantes :

- Efficacité et Vitesse : Une fenêtre de contestation typique de 7 jours peut être réduite à 1-3 jours (un challenger n'a plus besoin du temps supplémentaire pour identifier les soumissions malveillantes, créer une preuve et participer à plusieurs tours de procédures de contestation).
- Réduction des Coûts : L'utilisation des preuves ZK signifie que seules des informations minimales sur les transactions sont conservées, réduisant ainsi considérablement le coût des soumissions L2. Lorsqu'aucune contestation n'émerge, le coût de la soumission et de la vérification de la preuve ZK peut être ignoré. La RVP est donc plus économique que les rollups optimistes et ZK.

![Intégration Optimistic zkEVM](../../assets/docs/about/overview/opzk.png)

Visitez [Preuve de Validité Réactive](../how-morph-works/optimistic-zkevm) pour un article plus complet.

## Design Modulaire

Au cœur de Morph, une architecture de design modulaire sophistiquée est utilisée. La plateforme est organisée en trois modules fonctionnels (Réseau de Séquenceurs, Rollup, Optimistic zk-EVM), chacun défini par des rôles distincts qui collaborent dans diverses configurations pour répondre à des besoins variés. Chaque rôle au sein de ces modules fonctionne avec ses composants spécifiques, maintenant l'indépendance fonctionnelle. Cette structure modulaire favorise non seulement la flexibilité et l'adaptabilité, mais renforce également la composition du système. Elle permet un écosystème efficace et interactif, soutenant les divers besoins opérationnels de notre plateforme.

![Design Modulaire](../../assets/docs/about/overview/modu.png)

Visitez [Le Design Modulaire de Morph](../how-morph-works/2-morph-modular-design.md) pour un article plus complet.
