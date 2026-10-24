Déployer et gérer des services de domaine Active Directory

# Active Directory Domain Services (AD DS) — Synthèse

## 1. Définition

**Active Directory Domain Services (AD DS)** est un service d'annuaire centralisé permettant de gérer les identités et les ressources d'un réseau d'entreprise.

Il permet notamment :
- La gestion des utilisateurs, ordinateurs et groupes.
- L'authentification et l'autorisation.
- L'application de stratégies de sécurité (GPO).
- L'organisation et l'administration des ressources.

AD DS repose sur des **composants logiques** (organisation de l'annuaire) et **physiques** (serveurs, stockage et réseau).

## 2. Hiérarchie logique AD DS

| Composant | Définition |
|---|---|
| **Forêt** | Structure de niveau supérieur regroupant une ou plusieurs arborescences. |
| **Arborescence** | Ensemble de domaines partageant un espace de noms DNS continu. |
| **Domaine** | Conteneur logique regroupant les utilisateurs, ordinateurs, groupes et autres objets AD. |
| **Domaine racine de la forêt** | Premier domaine créé dans la forêt. |
| **OU** | Unité d'organisation permettant de regrouper des objets, déléguer l'administration et appliquer des GPO. |
| **Conteneur** | Regroupe des objets AD, mais ne permet pas de lier directement des GPO. |

### Exemple

```text
Forêt : contoso.com
│
├── Arborescence contoso.com
│   ├── contoso.com (domaine racine de la forêt)
│   │   ├── DC01
│   │   └── DC02
│   └── seattle.contoso.com (domaine enfant)
│
└── Arborescence adatum.com
    └── adatum.com (domaine racine d'arborescence)
```

Une forêt peut contenir plusieurs arborescences et domaines. En pratique, une organisation utilise généralement une seule forêt.

## 3. Base de données AD DS et réplication

La base de données AD DS est stockée sur les contrôleurs de domaine, notamment dans le fichier :

`C:\Windows\NTDS\ntds.dit`

Elle est divisée en **partitions**, contenant différentes informations.

| Partition | Contenu | Réplication |
|---|---|---|
| **Domaine** | Utilisateurs, groupes, ordinateurs et objets du domaine | Entre les DC du même domaine |
| **Schéma** | Définitions des types d'objets et de leurs attributs | Tous les DC de la forêt |
| **Configuration** | Informations de configuration de la forêt | Tous les DC de la forêt |

AD DS utilise principalement une **réplication multimaître** : plusieurs DC peuvent enregistrer des modifications qui sont ensuite synchronisées.

La forêt constitue une limite de réplication pour le schéma et la configuration, tandis que le domaine constitue la limite de réplication de sa partition de domaine.

## 4. Composants physiques

| Composant | Rôle |
|---|---|
| **Contrôleur de domaine (DC)** | Serveur hébergeant une copie de l'annuaire de son domaine et assurant l'authentification et la réplication. |
| **Magasin de données** | Base de données AD DS (`ntds.dit`) et journaux associés. |
| **Catalogue global (GC)** | Hébergé par un DC, permet de rechercher des objets dans tous les domaines de la forêt grâce à des informations partielles. |
| **RODC** | Contrôleur de domaine en lecture seule, notamment utilisé dans les filiales moins sécurisées. |
| **Site AD** | Représente une organisation physique du réseau, généralement basée sur les emplacements et la connectivité. |
| **Sous-réseau** | Plage d'adresses IP associée à un site AD. Un site peut comprendre plusieurs sous-réseaux. |

**Différences importantes :**
- Un domaine est une structure logique ; un DC est un serveur.
- Un domaine peut posséder plusieurs DC.
- Une OU organise les objets d'un domaine.
- Un site AD représente l'organisation physique du réseau, contrairement au domaine.

## 5. Authentification et autorisation

AD DS permet de contrôler l'accès aux ressources.

- **Authentification** : vérifier l'identité d'un utilisateur ou d'un ordinateur.
- **Autorisation** : déterminer les ressources auxquelles cette identité peut accéder.

Exemple : Alice se connecte avec son compte AD (authentification), puis ses permissions déterminent si elle peut accéder à un dossier partagé (autorisation).

Les **groupes AD** facilitent la gestion des permissions et des stratégies.

## 6. Administration et rôles FSMO

Certaines opérations AD DS sont assurées par des contrôleurs de domaine détenteurs de rôles particuliers : les **rôles FSMO**.

### Rôles uniques par forêt
- Maître de schéma.
- Maître d'attribution des noms de domaine.

### Rôles uniques par domaine
- Maître RID.
- Maître d'infrastructure.
- Émulateur PDC.

Le domaine racine de la forêt contient également les groupes **Administrateurs de l'entreprise** et **Administrateurs du schéma**.

Chaque domaine possède son groupe **Admins du domaine**.

## 7. Relations d'approbation (Trusts)

Une **relation d'approbation** établit un chemin d'authentification entre domaines ou forêts pour permettre l'accès à des ressources.

Dans une même forêt, les approbations entre domaines sont automatiquement :

- **Bidirectionnelles** : les domaines s'approuvent mutuellement.
- **Transitives** : si A approuve B et B approuve C, alors A approuve C.

| Type | Utilité |
|---|---|
| **Parent-enfant** | Relie un domaine parent et son domaine enfant. |
| **Racine d'arborescence** | Relie différentes arborescences d'une forêt. |
| **Externe** | Relie des domaines de forêts différentes. |
| **Forêt** | Établit une approbation entre deux forêts. |
| **Raccourci** | Optimise l'authentification entre domaines éloignés dans la structure. |
| **Realm** | Relie AD DS à un environnement Kerberos non-AD. |

**Important :** une relation d'approbation ne donne pas automatiquement accès aux ressources. Les autorisations restent nécessaires.

## 8. Points essentiels à retenir

1. **Forêt → Arborescence → Domaine → OU → Objets AD** : organisation logique simplifiée.
2. Le premier domaine créé devient le **domaine racine de la forêt**.
3. Chaque domaine peut posséder **plusieurs contrôleurs de domaine**.
4. Les DC d'un même domaine synchronisent leur annuaire par **réplication**.
5. Les domaines d'une forêt partagent un **schéma et une configuration communs**.
6. Le **catalogue global** permet les recherches à l'échelle de la forêt.
7. Les **sites et sous-réseaux** représentent l'organisation physique du réseau.
8. Les **GPO** permettent d'appliquer des paramètres de configuration et de sécurité.
9. Les **rôles FSMO** réservent certaines opérations à des DC particuliers.
10. Les **approbations** établissent des chemins d'authentification entre domaines, sans remplacer les autorisations.






### Déployer des contrôleurs de domaine AD DS

**Objectif :** installer, configurer et maintenir les contrôleurs de domaine (DC) pour assurer l'authentification et la disponibilité d'Active Directory.

#### 1. Installation d'un contrôleur de domaine

Le déploiement se fait en deux étapes :

1. **Installer le rôle AD DS** sur Windows Server.
2. **Promouvoir le serveur en contrôleur de domaine** avec l'assistant de configuration AD DS.

Installer le rôle seul ne suffit pas : le serveur n'est pas encore un DC.

#### 2. Paramètres importants lors de la promotion

- **Type de déploiement** : nouvelle forêt, nouveau domaine ou DC supplémentaire.
- **Nom DNS (FQDN)** : nom complet du domaine.
- **Niveaux fonctionnels** : déterminent les fonctionnalités disponibles et les versions de Windows Server compatibles.
- **DNS** : possibilité d'installer le rôle DNS sur le DC.
- **Catalogue global (GC)** : activé par défaut.
- **RODC** : DC en lecture seule, impossible comme premier DC d'une forêt.
- **Mot de passe DSRM** : utilisé pour les opérations de restauration AD DS.
- **Nom NetBIOS** : nom court du domaine.
- **Stockage** :
  - Base AD et journaux : `C:\Windows\NTDS`
  - SYSVOL : `C:\Windows\SYSVOL`

#### 3. Méthodes de déploiement

- **Windows Server avec interface graphique** : Gestionnaire de serveur ou Windows Admin Center.
- **Server Core** : PowerShell, Windows Admin Center ou outils d'administration distants (RSAT).
- **Installation à partir d'un support (IFM)** : réduit le trafic réseau lors de l'ajout d'un DC sur un site distant disposant d'une liaison WAN limitée.

#### 4. Contrôleurs de domaine en filiale : RODC

Un **RODC** est un contrôleur de domaine en lecture seule, adapté aux sites où la sécurité physique est limitée.

- Ne permet pas les modifications directes de l'annuaire.
- La **stratégie de réplication de mot de passe (PRP)** contrôle les identifiants pouvant être mis en cache.
- Les comptes privilégiés doivent rester exclus du cache.
- La **séparation des rôles administratifs** permet de déléguer la maintenance locale sans donner les droits d'administrateur du domaine.

#### 5. Mise à niveau des contrôleurs de domaine

Deux méthodes :

1. Mettre à niveau Windows Server sur un DC existant.
2. Ajouter un nouveau DC avec une version plus récente, puis retirer progressivement l'ancien.

**La seconde méthode est recommandée** dans la leçon, car elle permet de repartir sur une installation propre.

#### À retenir pour le lab

- Installer AD DS ≠ promouvoir un serveur en DC.
- Le premier DC crée la forêt et son domaine racine.
- Plusieurs DC peuvent assurer la disponibilité d'un domaine.
- DNS, catalogue global et DSRM sont des éléments importants du déploiement.
- Les RODC et l'installation IFM concernent surtout les environnements multisites.


### Sites AD DS et migration d'un contrôleur de domaine

**Objectif :** organiser les contrôleurs de domaine selon les emplacements physiques de l'entreprise afin de réduire la latence et le trafic réseau.

#### 1. Sites et sous-réseaux

- **Site AD** : représente un emplacement physique ou réseau (Paris, Lyon, etc.).
- **Sous-réseau AD** : plage d'adresses IP associée à un site.
- **Contrôleur de domaine** : peut être affecté à un site pour servir les utilisateurs de cet emplacement.

Un site peut contenir plusieurs sous-réseaux.

#### 2. Déployer un nouveau site

Trois étapes principales :

1. **Créer un site AD** dans *Sites et services Active Directory*.
2. **Associer un sous-réseau** au nouveau site.
3. **Déplacer le contrôleur de domaine** vers ce site dans la configuration AD.
  
Exemples PowerShell :

```powershell
# Créer un site
New-ADReplicationSite -Name "Lyon"

# Associer un sous-réseau au site
New-ADReplicationSubnet -Name "192.168.1.0/24" -Site "Lyon"

# Affecter un DC au nouveau site
Move-ADDirectoryServer -Identity "DC02" -Site "Lyon"
```

#### 3. Intérêt des sites AD

- Permettre aux clients d'utiliser des DC proches de leur emplacement.
- Réduire la latence d'authentification.
- Limiter les échanges inutiles sur les liaisons WAN.
- Organiser la réplication entre les différents sites.

**À retenir :** un site AD représente l'organisation physique du réseau, tandis qu'un domaine représente l'organisation logique des objets Active Directory.