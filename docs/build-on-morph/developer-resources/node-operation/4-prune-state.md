---
title: État de Prune
lang: fr-FR
---

La performance d'un nœud complet se dégrade lorsque la taille de stockage atteint un volume élevé. Nous suggérons que le nœud complet garde toujours un stockage léger en effectuant une taille de prune.

### Comment Pruner

1. Arrêtez le nœud, y compris le client de consensus (morphnode) et le client d'exécution (geth).
2. Exécutez ```nohup geth snapshot prune-zk-state --datadir "$GETH_DB_DIR" > prune.log &```. Cela prendra environ 5 à 7 heures pour finir.
3. Démarrez le nœud une fois terminé.

Le matériel est important, **assurez-vous que le SSD respecte : disque à état solide (SSD), 8k IOPS, débit de 500 Mo/s, latence de lecture < 1 ms.**

:::note
Pour pruner un nœud Geth, au moins 200 Go d'espace disque libre sont recommandés. Cela signifie que le prune ne peut pas être utilisé pour sauver un disque dur qui a été complètement rempli. Une bonne règle de base est de pruner avant que le nœud remplisse environ 80 % de l'espace disque disponible.
:::
