# Walkthrough de la quête [Utiliser GNU/Linux comme routeur IP](https://odyssey.wildcodeschool.com/quests/2350/pages/13710)

---
## Exercice - Etape 1
Créer 2 VM Debian, chacune avec 1 carte réseau. Mettre ces VMs dans virtual box en _réseau interne_, sur le _même réseau_.  
Première chose à faire pour chaque, éditer le fichier des cartes réseau `/etc/network/interfaces` pour conserver de façon durable le paramétrage. 

* Machine 1 :
>**iface enp0s3 inet static**   
>    **address 10.0.0.10/24**

:bulb: Explication : on indique la carte réseau enp0s3 dans mon cas. `inet` pour préciser que l'on est en ipv4. `static` pour indiquer que l'adresse sera fixe.)
On fait la même chose pour l'ipv6 :

>**iface enp0s3 inet6 static**  
>    **address fd8f:2d0f:0240::10/64**

:bulb: Explication : `inet6` pour indiquer l'ipv6. Pour le réseau en ipv6 j'ai utilisé [le générateur d'adresses Unicast locales uniques](https://www.unique-local-ipv6.com/). Les adresses IPv6 unicast locales uniques, permettent de communiquer sur un réseau interne et sont routables entre les réseaux mais ne peuvent pas aller sur internet.  


* Machine 2 :
>**iface enp0s3 inet static**  
>   **address 10.0.0.11/24**

>**iface enp0s3 inet6 static**  
>    **address fd8f:2d0f:0240::11/64**

Il faut bien penser à redémarrer les cartes réseau sur les 2 machines avec la commande :
`systemctl restart networking.service`


:heavy_exclamation_mark: Il y a une autre façon permet de faire la même chose mais de façon temporaire, c'est à dire valable tant que l'on ne redémarre pas la machine. C'est avec la commande `ip`. Dans mon cas je préfère modifier le fichier de configuration, je n'irai pas plus loin avec la commande `ip`. :blush:

Il faut bien sûr pinger entre chaque machine et avec les 2 formes d'IP.

Voici la solution pour : Machine 1 :arrow_right: Machine 2.
>**`ping 10.0.0.11`**  
>**`ping fd8f:2d0f:0240::11`**  
Il faut tester également de le Machine 2 :arrow_right: Machine 1 ...
Lorsque tout fontionne nous pouvons passer à l'étape 2.  


## Exercice - Etape 2

Il faut créer notre routeur :
Créer une VM Debian. Lui attribuer 2 cartes réseau et les mettre en _réseau interne_, sur un _réseau différent_.
Nous allons éditer la config des 2 cartes réseaux comme demandé dans la quête. C'est à dire une carte sur le même réseau que les premières machines et une carte sur un réseau différent :

Carte sur le réseau des premières
>**iface enp0s3 inet static**  
>    **address 10.0.0.1/24**  
>**iface enp0s3 inet6 static**  
>    **address fd8f:2d0f:0240::1/64**  


Carte sur un réseau différent :
>**iface enp0s8 inet static**  
>    **address 192.168.0.250/24**  
>**iface enp0s8 inet6 static**  
>    **address fd8f:2d0f:0240:192::250/64**  

### Activation permanente de l'IP forwarding sous Linux
L'IP forwarding permet à un système d'exploitation (ici Linux) de faire suivre des paquets comme le fait un routeur ou plus généralement de les router au travers d'autres réseaux.
Le fichier a éditer est :  `/etc/sysctl.conf`.  
Il faut décommenter ces 2 lignes, respectivement pour l'IPv4 et l'IPv6 :  
>**net.ipv4.ip_forward=1**  
>**net.ipv6.conf.all.forwarding=1**  
Enregistrer et redémarer le service réseau :
`systemctl restart networking.service`












