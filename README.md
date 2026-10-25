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
1) un Dockerfile est préférable à la config manuelle car il décrit l'env sous forme de code: la construction est automatique et reproductible ( même résultat sur toute machine).
2) une image docker est un modèle figé qui contient tout ce qu'il faut pour exécuter une appli ( dépendances, config, appli ...). Elle est construite à partir du dockerfile et ne change pas une fois créée. Un conteneur est une instance en cours d'exécution de cette image ( on peut créer plusieurs conteneurs indépendants à partir d'une même image).

#### Etape 4
1) Docker Compose est préférable au lancement manuel car il permet de démarrer, arrêter et reconstruire tous les conteneurs d’une application en une seule commande (docker compose up / down). De plus, la configuration de tous les services d'une application est regroupée dans un fichier donc on a moins de commande à saisir, moins d’erreurs et un déploiement reproductible.
2) docker-compose.yml décrit les services de l’application et leur configuration. C'est le fichier sur lequel Docker Compose s'appuie pour créer et lancer les conteneurs.
3) Docker Compose atteint ses limites dès qu’on sort d’une seule machine donc quand on doit répartir les conteneurs sur plusieurs machines.
## TP2
### Checkpoints
#### Etape 1
1) Le réseau privé permet aux VM au sein de ce même réseau de communiquer entre elles tout en étant isolés des autres client du Cloud. Le routeur externe relie le réseau privée au réseau publique. Il sert de passerelle pour que les VM accèdent à Internet (NAT) et permet de les rendre joignables depuis l'extérieur grace aux IP flottantes.
2) Un fournisseur Cloud propose de nombreuses catégories de ressources pour offrir un maximum de flexibilité à ses utilisateurs. Son offre est découpée en brique indépendantes : calcul, stockage et réseau. Chaque client peut alors composer l'infrastructure adaptée à ses besoins. Ce découpage permet aussi au fournisseur de gérer la facturation par type de ressources.
3) Un paquet envoyé depuis l'extérieur a pour destination l'IP flottante associée à la VM. Il traverse Internet depuis le réseau externe du Cloud jusqu'au routerdefault. Le routeur remplace alors l'IP flottante par l'adresse privée de la VM . Il transmet ensuite le paquet via son interface 192.168.10.1 sur le réseau net-discovery. Avant d'atteindre la VM, le paquet est filtré par le groupe de sécurité.
   
#### Etape 2

1) Pour se connecter en SSH à une nouvelle VM, il faut :
   
               1- La placer sur un réseau privé relié au routeur externe
               2- Lui associer un groupe de sécurité autorisant SSH (TCP 22)
               3- Créer une paire de clés à la création de l'instance et télécharger la clé privée
               4- Lui associer une IP flottante
               5- Lancer depuis la machine hote : ssh -i nom_cle.pem <login>@<IPflottante>

3) Adresse IP privée : C'est l'identité de la VM au sein du réseau privé, utilisée pour communiquer avec les autres VM et avec le routeur. Elle n'est pas joignable depuis Internet. Dans la connexion SSH, c'est la destination finale du paquet une fois qu'il est entré dans le réseau privé.
   
    Adresse IP flottante : c'est une adresse publique, gérée par le routeur et associée logiquement à une VM. C'est le point d'entrée depuis l'extérieur car la machine hote se connecte à cette adresse et le routeur traduit l'IP flottante en IP privéee de la VM.

    Groupe de sécurité : Une sorte de firewall appliquée directement à la VM. Un ensemble de règles qui autorisent ou bloquent des flux. Le traffic entrant étant bloqué par défaut, il doit contenir une règle autorisant TCP sur le port 22 pour que la connexion SSH soit acceptée.

4) Openstack distingue les adresses IP privées et les adresses IP flottantes publiques pour économiser les adresses publiques tout en assurant la connectivité réseau. Les machines virtuelles communiquent entre elles grace à leurs adresses privées et peuvent accèder à Internet via le routeur utilisant le NAT. Une IP flottante est attribuée uniquement aux machines virtuelles qui doivent etre accessible depuis l'extérieur.
