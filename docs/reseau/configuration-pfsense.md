# Installation et configuration de pfSense

Cette configuration fait suite à la [préparation des réseaux et des interfaces dans VMware](configuration-vmware.md).

## Installation de pfSense CE

L'installateur propose l'option **Install CE** pour installer pfSense Community Edition.

![Choix de pfSense CE dans l'installateur Netgate](images/pfsense/installation-pfsense-ce.webp)

## Interfaces et adresses dans pfSense

La console pfSense affiche les interfaces WAN, LAN et OPT ainsi que leurs adresses IP.

![Interfaces et adresses IP dans la console pfSense](images/pfsense/pfsense-interfaces.png)

## Règles de pare-feu

Les règles d'autorisation ci-dessous ont été ajoutées sur OPT1 et OPT2 : elles n'étaient pas présentes par défaut sur cette interface.

![Règles sur OPT1 : blocage vers OPT3 subnets et autorisation depuis OPT1 subnets](../problemes-rencontres/images/ping-dc/regles-corrigees.png)

Le diagnostic associé est détaillé dans [Problème de ping depuis DC01](../problemes-rencontres/ping-dc.md).
