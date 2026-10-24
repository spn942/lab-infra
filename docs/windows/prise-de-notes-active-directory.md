Niveau le plus élevé : Forêt 
Domaine le plus élevé : domaine racine de la forêt 

Une forêt peut contenir plusieurs arborerscence : plusieurs domaines bien que ce soit rare

forêt = conteneur de niveau principal 

En entreprise, je travaille sur un domaine enfant d'une arboerscence qui n'est peut être pas la seule.

relations d'approbations







## Gérer les maîtres d'opérations AD DS (FSMO)

### 1. Principe des rôles FSMO

Active Directory utilise une **réplication multimaître** : plusieurs contrôleurs de domaine (DC) peuvent modifier l'annuaire et synchroniser leurs changements.

Cependant, certaines opérations doivent être réalisées par **un seul DC à la fois** pour éviter les conflits.

Ces opérations sont confiées aux **5 rôles FSMO** (*Flexible Single Master Operations*).

Par défaut, le premier DC d'une nouvelle forêt possède les cinq rôles. Ils peuvent ensuite être répartis entre plusieurs DC.

### 2. Les cinq rôles FSMO

**Deux rôles uniques par forêt :**

| Rôle | Fonction |
|---|---|
| **Maître de schéma** | Gère les modifications du schéma Active Directory. |
| **Maître d'attribution des noms de domaine** | Gère l'ajout, la suppression et le renommage des domaines de la forêt. |

**Trois rôles uniques par domaine :**

| Rôle | Fonction |
|---|---|
| **Maître RID** | Distribue des blocs d'identifiants RID aux DC afin de garantir l'unicité des SID des objets. |
| **Maître d'infrastructure** | Maintient les références aux objets provenant d'autres domaines. |
| **Émulateur PDC** | Gère notamment la synchronisation de l'heure, les changements urgents de mots de passe et les modifications des GPO. |

### 3. Gestion des rôles FSMO

Il existe deux façons de déplacer un rôle FSMO :

- **Transfert** : déplacement planifié d'un rôle entre deux DC disponibles.
- **Saisie (seizure)** : récupération forcée d'un rôle lorsque son détenteur est définitivement indisponible.

**La saisie est une opération de dernier recours.**

### 4. Commandes PowerShell

Afficher les informations de la forêt et ses détenteurs de rôles FSMO :

```powershell
Get-ADForest
```

Afficher les informations du domaine et ses détenteurs de rôles FSMO :

```powershell
Get-ADDomain
```

Transférer un rôle FSMO vers un autre contrôleur de domaine :

```powershell
Move-ADDirectoryServerOperationsMasterRole -Identity "DC02" -OperationsMasterRole PDCEmulator
```

En cas de panne irrécupérable du détenteur, une saisie peut être effectuée avec l'option `-Force`.

### 5. À retenir

- AD DS possède **5 types de rôles FSMO**.
- **2 rôles sont uniques par forêt**, **3 par domaine**.
- Un DC peut posséder plusieurs rôles FSMO.
- Le premier DC d'une nouvelle forêt possède initialement les cinq rôles.
- Les rôles peuvent être transférés vers d'autres DC.
- La saisie d'un rôle est réservée aux situations d'urgence.
(Pour restaurer lad BD AD DS, on démarre le contrôleur de domaine en mode DSRM via les paramètres de démarrage avancés, notion de catalogue global vue aussi)
