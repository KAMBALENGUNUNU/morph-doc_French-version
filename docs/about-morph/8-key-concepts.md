---
title: Concepts Clés
lang: fr-FR
keywords: [morph,layer2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution optimistic zk-rollup sécurisée, décentralisée et performante. Essayez-le maintenant !
---

## Rollups Optimistes

Les rollups optimistes sont une solution de mise à l'échelle de Layer 2 pour les blockchains qui améliorent le débit des transactions et réduisent les coûts en supposant que les transactions sont valides et en ne les vérifiant que si un défi est soulevé. Cette méthode repose sur une période de contestation pendant laquelle les validateurs peuvent contester des transactions qu'ils estiment incorrectes. Si aucune contestation n'est soulevée, les transactions sont considérées comme finales. Les rollups optimistes améliorent considérablement l'évolutivité tout en maintenant la sécurité, ce qui en fait une solution efficace pour gérer un volume plus élevé de transactions sur les réseaux blockchain.

[En savoir plus sur les Rollups Optimistes](https://ethereum.org/en/developers/docs/scaling/optimistic-rollups/)

## Rollups ZK

Les rollups ZK, ou rollups à connaissance nulle, sont une solution de mise à l'échelle de Layer 2 qui utilise des preuves cryptographiques pour vérifier la validité des transactions hors chaîne avant de les regrouper et de soumettre une preuve à la blockchain principale. Chaque lot de transactions est accompagné d'une preuve à connaissance nulle, qui garantit que toutes les transactions du lot sont valides sans révéler les données sous-jacentes. Cette méthode offre une finalité immédiate et une grande sécurité, car la chaîne principale n'a besoin de vérifier que la preuve et non chaque transaction individuelle, réduisant ainsi considérablement la charge de calcul et améliorant l'évolutivité.

[En savoir plus sur les Rollups ZK](https://ethereum.org/en/developers/docs/scaling/zk-rollups/)

## Séquenceurs

Les séquenceurs sont des nœuds spécialisés responsables de l'ordonnancement et du regroupement des transactions dans des solutions de mise à l'échelle de Layer 2 comme les rollups. Ils jouent un rôle crucial dans la détermination de la séquence des transactions, la création de blocs et l'engagement périodique de ces blocs à la blockchain principale. Dans les systèmes décentralisés, plusieurs séquenceurs travaillent ensemble pour renforcer la sécurité et éviter les points de défaillance uniques. En garantissant que les transactions sont traitées efficacement et en toute sécurité, les séquenceurs aident à maintenir l'intégrité et la performance des réseaux de Layer 2.

## Preuve de Fraude

La preuve de fraude est un mécanisme utilisé dans les solutions de mise à l'échelle blockchain comme les rollups optimistes pour garantir la validité des transactions. Lorsqu'un séquenceur soumet un lot de transactions, celles-ci sont supposées valides sauf contestation. Pendant une période de contestation désignée, tout validateur ou participant au réseau peut soumettre une preuve de fraude s'il détecte une transaction incorrecte. Cette preuve implique la vérification des données de la transaction et la démonstration de l'erreur à la blockchain principale. Si la preuve de fraude est validée, la transaction incorrecte est rejetée, garantissant l'intégrité et la sécurité du réseau tout en minimisant les coûts de calcul.

## Preuve de Validité

La preuve de validité est une méthode cryptographique utilisée pour garantir que les transactions au sein d'un rollup sont correctes avant qu'elles ne soient finalisées sur la blockchain principale. Dans les systèmes comme les rollups ZK, chaque lot de transactions est accompagné d'une preuve de validité qui vérifie la correction de toutes les transactions du lot. Cette approche améliore la sécurité et l'efficacité en éliminant le besoin de vérification individuelle des transactions sur la chaîne principale, offrant une finalité immédiate et réduisant les coûts de calcul.

## zkEVM

Le zkEVM, ou Zero-Knowledge Ethereum Virtual Machine, est une implémentation avancée de la machine virtuelle Ethereum qui intègre des preuves à connaissance nulle pour améliorer l'évolutivité et la sécurité. En utilisant des preuves zk, le zkEVM permet la validation des transactions hors chaîne, garantissant que seules les transitions d'état valides sont soumises à la chaîne principale. Cette méthode offre un débit élevé et des coûts de transaction réduits tout en maintenant la sécurité et l'absence de confiance d'Ethereum.

## Signatures BLS

Les signatures BLS (Boneh-Lynn-Shacham) sont une technique cryptographique utilisée pour agréger plusieurs signatures en une seule signature compacte. Cela est particulièrement utile dans les réseaux blockchain pour réduire la taille des données et améliorer l'efficacité de la vérification des transactions. Les signatures BLS permettent à plusieurs validateurs de signer un message collectivement, ce qui donne une seule signature qui peut être vérifiée rapidement et de manière rentable, améliorant ainsi l'évolutivité globale du réseau.

## Disponibilité des Données

La disponibilité des données fait référence à la garantie que toutes les données nécessaires pour vérifier les transactions blockchain sont accessibles et récupérables. Dans le contexte des rollups, garantir la disponibilité des données est crucial pour maintenir l'intégrité et la sécurité des transactions hors chaîne. Cela garantit que quiconque peut télécharger et vérifier les données utilisées dans les preuves de rollup, empêchant des scénarios où les transactions sont finalisées sans possibilité de vérification.

## EIP - 4844

L'EIP-4844, également connu sous le nom de Proto-Danksharding, est une proposition d'amélioration d'Ethereum visant à introduire un nouveau type de transaction qui réduit les coûts de données et améliore l'évolutivité. Cela implique d'ajouter un nouveau format de transaction capable de gérer efficacement de grandes quantités de données, préparant le terrain pour de futures implémentations de sharding. Cette proposition améliore la capacité du réseau à gérer les données plus efficacement, contribuant aux améliorations globales du débit et de l'efficacité des coûts.

[Découvrez comment l'EIP-4844 impacte Morph et d'autres rollups.](https://www.eip4844.com/)
