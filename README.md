# Lab Infra Hybride AD/Entra ID

Ce laboratoire a pour objectif de revoir Windows Server en ajoutant les notions de la certification AZ-802.

Du réseau sera également intégré pour revoir ce que j'ai fait en formation et acquérir de nouvelles compétences.

Dans un second temps, toujours en suivant les modules de préparation à cette certification, l'objectif sera de découvrir Azure, voire de l'administrer (AZ-104).

Enfin, bien plus tard, je souhaiterais découvrir et comprendre le DevOps, ou essayer de mettre en place certains workflows en lien avec les outils de ticketing / logiciels de gestion des identités, notamment pour la gestion des onboardings ou des tâches pouvant être automatisées.


## Technologies utilisées

- VMware Workstation
- pfSense
- Windows Server 2022
- Active Directory Domain Services (AD DS)
- Windows 11
- Linux	

**Prévues :** GNS3, Microsoft Azure.

## Documentation

- [Feuille de route](docs/feuille-de-route/route.md)

### Réseau

- [Plan d'adressage](docs/reseau/plan-adressage.md)
- [Raisonnement du plan d'adressage](docs/reseau/raisonnement-plan-adressage.md)
- [Configuration réseau VMware](docs/reseau/configuration-vmware.md)
- [Installation et configuration de pfSense](docs/reseau/configuration-pfsense.md)

### Windows Server et Active Directory

- [Installation et configuration de DC01](docs/windows/installation-dc01.md)
- [Installation d'AD DS et promotion en contrôleur de domaine](docs/windows/installation-active-directory.md)
- [Jonction d'un client au domaine](docs/windows/joindre-le-domaine.md)
- [Commandes PowerShell utiles](docs/windows/commandes-powershell-utiles.md)
- [Prise de notes Active Directory](docs/windows/prise-de-notes-active-directory.md)

### Problèmes rencontrés

- [Diagnostic et résolution du problème de ping depuis DC01](docs/problemes-rencontres/ping-dc.md)

### Révisions

- [AZ-802 : déployer et gérer AD DS](docs/revisions/az-802/01-deploiement-et-gestion-ad-ds.md)
