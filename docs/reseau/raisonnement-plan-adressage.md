
# Plan d'adressage

On utilise un pool d’adresses IP privées non routables sur Internet, défini par la RFC 1918.

## Pourquoi utiliser des VLAN et des sous-réseaux ?

### VLAN

- Segmenter le réseau au niveau 2 ;
- Séparer les domaines de broadcast (niveau 2) ;
- Permettre d’appliquer des règles de sécurité entre les VLAN via un routeur/firewall.

### Sous-réseaux

- Organiser l’adressage IP ;
- Séparer les réseaux au niveau 3 ;
- Limiter la portée des broadcasts (niveau 3) ;
- Permettre l’agrégation de routes afin de réduire le nombre d’entrées dans les tables de routage et de simplifier le routage.

Pour ce lab, on utilisera du FLSM afin de rester proche de ce qui a été vu en formation. Le VLSM pourra être étudié plus tard.

## Réseau

J'ai voulu à peu près 1 000 machines pour être large et pouvoir faire du découpage réseau.

10.0.0.0/22 = avec un slash 22, ma plage va de 10.0.0.0 à 10.0.3.255, pour 1 024 machines (2 à la puissance du nombre de bits à 0) et .3 car tous les bits du masque sont à 1, jusqu'aux deux derniers bits du dernier octet.

Les deux derniers bits du 3ᵉ octet peuvent prendre les valeurs 00, 01, 10 ou 11, ce qui donne respectivement 0, 1, 2 ou 3.

Ne sachant pas exactement de combien de machines j'aurai besoin pour chaque sous-réseau, je vais faire du FLSM. Pour diviser mon réseau en quatre sous-réseaux, j'emprunte alors deux bits :

Réseau principal (on premise) : 10.0.0.0/22, mon premier réseau devient alors : 10.0.0.0/24. Le dernier bit à 1 équivaut à la valeur "1" sur mon tableau, donc mon saut entre les réseaux sera de 1 sur le 3e octet.

### Sous-réseaux

Sous-réseau dédié aux postes : 10.0.0.0/24, broadcast : 10.0.0.255

Sous-réseau dédié aux serveurs : 10.0.1.0/24, broadcast : 10.0.1.255

Sous-réseau dédié à l'administration réseau : 10.0.2.0/24, broadcast : 10.0.2.255

Sous-réseau dédié à ma DMZ : 10.0.3.0/24, broadcast : 10.0.3.255

### Azure

Réseau principal : 10.10.0.0/22

| Usage | Sous-réseau | Broadcast |
|---|---|---|
| Postes | 10.10.0.0/24 | 10.10.0.255 |
| Serveurs | 10.10.1.0/24 | 10.10.1.255 |
| Administration réseau | 10.10.2.0/24 | 10.10.2.255 |
| DMZ | 10.10.3.0/24 | 10.10.3.255 |

## Sources

- https://racine.gatoux.com/lmdr/index.php/ladressage-ip/
- https://www.it-connect.fr/chapitres/cisco-ios-determiner-le-plan-adressage-nouveau-reseau/
