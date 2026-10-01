On utilise un pool d’adresses IP privées non routables sur Internet,

défini par la RFC 1918.



Pourquoi utiliser des VLAN et des sous-réseaux ?



\- VLAN :

&#x20; - segmenter le réseau au niveau 2 ;

&#x20; - séparer les domaines de broadcast (niveau 2) ;

&#x20; - permettre d’appliquer des règles de sécurité entre les VLAN via un routeur/firewall.



\- Sous-réseaux :

&#x20; - organiser l’adressage IP ;

&#x20; - séparer les réseaux au niveau 3 ;

&#x20; - limiter la portée des broadcasts (niveau 3) ;

&#x20; - permettre l’agrégation de routes afin de réduire le nombre

&#x20;   d’entrées dans les tables de routage et de simplifier le routage.



Pour ce lab, on utilisera du FLSM afin de rester proche de ce qui a été vu

en formation. Le VLSM pourra être étudié plus tard.





Réseau :



10.0.0.0/22 = avec un slash 22, ma plage va de 10.0.0.0 à 10.0.3.255, pour 1024 machines (2 exposé à nombre de bits à 0) et .3 car tous les bits du masque sont à zéro, jusqu'au dernier octet où le premier bit (qui représente la valeur 1) et le 2e bit (qui représente la valeur 2). Il n'y a alors que deux slots, le 3e octet peut donc prendre la valeur 00000000 soit 0, 00000001 soit 1, 00000010 soit 2, ou 00000011 soit 3.





Ne sachant pas exactement de combien de machines j'aurais besoin pour chaque sous-réseau, je vais faire du FLSM, pour diviser mon réseau en quatre sous réseaux, j'emprunte alors deux bits :



Réseau principal (on premise): 10.0.0.0/22, mon premier réseau devient alors : 10.0.0.0/24. Le dernier bit à 1 équivaut à la valeur un sur mon tableau, donc mon saut entre les réseau sera de 1 sur le 3e octet.



Sous réseau dédié aux postes : 10.0.0.0/24, broadcast : 10.0.0.255

Sous réseau dédié aux serveurs : 10.0.1.0/24, broadcast : 10.0.1.255

Sous réseau dédié à l'administration réseau : 10.0.2.0/24, broadcast : 10.0.2.255

Sous réseau dédié à ma DMZ : 10.0.3.0/24, broadcast : 10.0.3.255




### Azure

Réseau principal : 10.10.0.0/22

| Usage | Sous-réseau | Broadcast |
|---|---|---|
| Postes | 10.10.0.0/24 | 10.10.0.255 |
| Serveurs | 10.10.1.0/24 | 10.10.1.255 |
| Administration réseau | 10.10.2.0/24 | 10.10.2.255 |
| DMZ | 10.10.3.0/24 | 10.10.3.255 |






sources : https://racine.gatoux.com/lmdr/index.php/ladressage-ip/

&#x09;  https://www.it-connect.fr/chapitres/cisco-ios-determiner-le-plan-adressage-nouveau-reseau/

