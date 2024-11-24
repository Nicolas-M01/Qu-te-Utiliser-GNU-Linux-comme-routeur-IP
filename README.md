### Walkthrough de la quête [Utiliser GNU/Linux comme routeur IP](https://odyssey.wildcodeschool.com/quests/2350/pages/13710)


#### Exercice - Etape 1
Créer 2 VM Debian, chacune avec 1 carte réseau. Mettre ces VMs dans virtual box en _réseau interne_, sur le _même réseau_.  
Première chose à faire pour chaque, éditer le fichier des cartes réseau `/etc/network/interfaces` pour conserver de façon durable le paramétrage. 

* Machine 1 :
>**iface enp0s3 inet static**  
>    **address 10.0.0.10/24**

Explication : on indique la carte réseau enp0s3 dans mon cas. `inet` pour préciser que l'on est en ipv4. `static` pour indiquer que l'adresse sera fixe.)
On fait la même chose pour l'ipv6 :

>**iface enp0s3 inet6 static**  
>    **address fd8f:2d0f:0240::10/64**

Explication : `inet6` pour indiquer l'ipv6. Pour le réseau en ipv6 j'ai utilisé [le générateur d'adresses Unicast locales uniques](https://www.unique-local-ipv6.com/). Les adresses IPv6 unicast locales uniques, permettent de communiquer sur un réseau interne et sont routables entre les réseaux mais ne peuvent pas aller sur internet.

Une autre façon permet de faire la même chose mais de façon temporaire, c'est à dire valable tant que l'on ne redémarre pas la machine. C'est avec la commande `ip`. Dans mon cas je préfère modifier le fichier de configuration, je n'irai pas plus loin avec la commande `ip`
