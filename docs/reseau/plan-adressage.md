# Plan d'adressage

On utilise un pool d’adresses IP privées non routables sur Internet,
défini par la RFC 1918.

## Réseau principal

Réseau principal : 10.0.0.0/22

Plage : 10.0.0.0 à 10.0.3.255

## Sous-réseaux

| Usage | Sous-réseau | Broadcast |
|---|---|---|
| Postes | 10.0.0.0/24 | 10.0.0.255 |
| Serveurs | 10.0.1.0/24 | 10.0.1.255 |
| Administration réseau | 10.0.2.0/24 | 10.0.2.255 |
| DMZ | 10.0.3.0/24 | 10.0.3.255 |


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