### Walkthrough de la quête Utiliser GNU/Linux comme routeur IP

#### Exercice - Etape 1
Créer 2 VM Debian, chacune avec 1 carte réseau. Mettre ces VMs dans virtual box en réseau interne, sur le même réseau.  
Première chose à faire pour chaque, éditer le fichier des cartes réseau `/etc/network/interfaces` pour conserver de façon durable le paramétrage. 




une autre façon permet de faire la même chose mais de façon temporaire, c'est à dire valable tant que l'on ne redémarre pas la machine. C'est avec la commande `ip`. Dans mon cas je préfère modifier le fichier de configuration, je n'irai pas plus loin avec la commande `ip`
