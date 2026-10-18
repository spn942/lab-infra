### Installation de Windows Server 2022

- Je crée une nouvelle VM depuis **File → New Virtual Machine**.
- Je sélectionne **« I will install the operating system later »** pour que VMware n'utilise pas Easy Install.
- Je sélectionne **Windows Server 2022** comme système d'exploitation.
- Je configure les ressources de la VM : **2 vCPU, 4 Go de RAM et 60 Go de stockage**.
- Je connecte la VM au réseau serveurs **VMnet3**.
- Je monte l'ISO de Windows Server 2022 et lance l'installation.
- Je sélectionne **Windows Server 2022 Standard Evaluation (Desktop Experience)** pour disposer d'une interface graphique.
- Je définis le mot de passe Administrateur et termine l'installation.


### Configuration de Windows Server 2022

- Je renomme le serveur **DC01**.
- Je configure son adresse IP statique : **10.0.1.10/24**, avec la passerelle **10.0.1.1** et le DNS **10.0.1.10**.























Sources : https://learn.microsoft.com/fr-fr/training/modules/deploy-manage-active-directory-domain-services-domain-controllers/2-define-active-directory-domain-services