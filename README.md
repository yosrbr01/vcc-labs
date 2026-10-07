# vcc-labs
## TP1
### Checkpoints
#### Etape 1
1) Une machine virtuelle est une machine logicielle disposant des mêmes proprités qu'une machine physique ( processeur, mémoire , disque, os ...). Elle est hébergée sur une machine hôte dont elle utilise une partie des ressources physiques, tout en étant isolée des autres VMs préssentes. La communication entre la VM et l'hôte ainsi que la gestion de la VM se fait via un hypserviseur.
2)  Avantages de la virtualisation dans un environnement professionnel:
  - La compromission d'une VM n'induit pas la compromission des autres => plus de sécurité
  - La mutualisation des ressources => meilleure utilisation du matériel disponible

3) de notre point de vue en tant qu'utilissateurs on dispose de 2 cas d'usage:
   - soit la vm est directement hébergée sur la machine physique qu on utilise ( cas du tp1) dans quel cas on n'observe pas de différnce réelle mis à part l'établissement de la connexion ssh (qui n'est pas obligatoire)
   - soit la vm est hébergée sur le cloud et la on peut observer des différences puisque la connexion se fait à distance. On pourrait avoir plus de latence, dépendre de la qualité du réseau... Par contre, la VM reste accessible depuis n'importe quel poste et ses ressources ne dépendent pas de celles de notre ordinateur.

#### Etape 2
1) Un conteneur docker est un environnement d'exécution isolé qui regroupe une application et tout ce dont elle a besoin ( bibliothèques, dépendances, configs). Il est créé à partir d'une image et géré par le moteur Docker.
2) L'isolation dans une machine virtuelle se fait au niveau matériel: chaque VM embarque son propre OS et repose sur l'hyperviseur. En contrepartie, l'isolation d'un conteneur se fait au niveau du noyau : les conteneurs partagent le noyau de l'OS hôte.
3) Les conteneurs sont adaptés au Cloud car sont légers, portables et rapides à démarrer. Ce qui permet de déployer et de multiplier une appli avec toutes ses dépendances sur n'importe quel serveur.

#### Etape 3
