---
title: Cycle de Vie des Transactions
lang: fr-FR
keywords: [morph,ethereum,rollup,couche2,preuve de validité,optimistic zk-rollup]
description: Améliorez votre expérience blockchain avec Morph - la solution de zk-rollup optimiste, sécurisée, décentralisée et à coût efficace. Essayez-la maintenant!
---

## Comment une transaction L2 est-elle traitée sur Morph

1. Soumettre la Transaction
   
Les transactions initiées par l'utilisateur sont d'abord envoyées à la mempool du nœud L2, où elles attendent d'être sélectionnées et traitées par un séquenceur.

2. Consensus de Transaction
   
Au sein du réseau de séquenceurs, les transactions subissent un processus de consensus. Un séquenceur sélectionné propose un bloc contenant la transaction, puis envoie les blocs au niveau de consensus (client de consensus).

D'autres séquenceurs valident ensuite ce bloc en exécutant ce bloc, vérifiant effectivement la légitimité de la transaction.

3. Exécution de la Transaction
   
Une fois tous les votes sur le bloc finalisés, chaque séquenceur et nœud appliquera ce bloc pour mettre à jour son état local.
   
4. Regroupement de Transactions
   
Lorsque le point de regroupement est atteint, chaque séquenceur devra construire le lot avec tous les blocs consensuels pour la dernière époque, le lot passera par un consensus nécessitant la signature de chaque séquenceur, toutes les signatures seront agrégées avec une signature BLS.
   
5. Séquençage de Lots
   
Le [séquenceur sélectionné](../general-protocol-design/1-rollup.md) s'engagera à soumettre les lots au contrat Rollup de la Couche 1 pour la vérification et pour garantir la disponibilité des données.
   
6. Vérification de Lot
   
Un lot (tout comme les transactions au sein du lot) passera d'abord par la vérification de la signature BLS par le contrat rollup pour confirmer les résultats du consensus L2, puis un lot passera par une [période de contestation](../3-optimistic-zkevm.md) pour être marqué comme finalisé, solidifiant leur statut au sein de l'état L1 et L2.

## Statut de la Transaction Morph

### Traitement​

Une fois soumise, une transaction entre dans la phase de consensus gérée par les séquenceurs et est placée dans un bloc pré-exécution.

### Confirmée​

Après l'exécution par le séquenceur, l'état mis à jour de la transaction est local à L2. Il est ensuite regroupé et envoyé à L1, où il doit subir une période de contestation avant la finalisation.

### Sûre

Le lot contenant la transaction est soumis à la Couche 1 mais n'est pas encore finalisé.

### Finalisée​

Une transaction est considérée comme finalisée après avoir survécu à la période de contestation ou avoir été vérifiée par une preuve à connaissance nulle (ZK-Proof). Ce n'est qu'alors qu'elle est officiellement intégrée dans l'état final L1 et L2.
