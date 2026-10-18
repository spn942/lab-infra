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

## Attribution des adresses IP

### Passerelles

| Réseau | Adresse IP | Équipement |
|---|---|---|
| Postes | 10.0.0.1 | pfSense |
| Serveurs | 10.0.1.1 | pfSense |
| Administration réseau | 10.0.2.1 | pfSense |
| DMZ | 10.0.3.1 | pfSense |

### Serveurs et machines

| Machine | Adresse IP | Réseau | Attribution |
|---|---|---|---|
| DC01 | 10.0.1.10 | Serveurs | Statique |
| SRV01 (prévu) | 10.0.1.20 | Serveurs | Statique |
| LINUX01 (prévu) | 10.0.1.30 | Serveurs | Statique |
| TICKETING1 (prévu) | 10.0.1.40 | Serveurs | Statique |
| ADMIN01 (prévu) | 10.0.2.10 | Administration réseau | Statique |
| CLIENT01 (prévu) | 10.0.0.1 | Postes | DHCP |

### Convention d'adressage du réseau serveurs

| Plage | Utilisation |
|---|---|
| 10.0.1.1 | Passerelle pfSense |
| 10.0.1.2 à 10.0.1.9 | Adresses réservées |
| 10.0.1.10 à 10.0.1.19 | Contrôleurs de domaine |
| 10.0.1.20 à 10.0.1.99 | Autres serveurs |

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