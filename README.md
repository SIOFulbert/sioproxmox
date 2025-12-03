# SIO Proxmox
Ce dépôt contient certains scripts et fichiers utiles pour l'administration des infrastructures Proxmox de BTS SIO de Centre Val de Loir.



## Scripts

### sync-etudiants-pool
Ce script permet la création de pools personnels pour les nouveaux étudiants membres du groupe proxmox dédié aux étudiant. Il marque également les pools des membres qui n'existent plus dans le groupe comme supprimés.

Par défaut le script crée des pools commençant par « étudiant- » et se base sur le groupe « proxmox-etudiant ». Il renomme les pools étudiants obsolètes avec le préfixe "removed-".
Vous pouvez modifier les variables du script pour changer son comportement :
- REALM : Nom du royaume proxmox (Active Directory) dont est issu le groupe étudiant (défaut "adsio")
- GROUP : Nom du groupe étudiant dans l'Active Directory (défaut "proxmox-etudiant")
- ROLE : Nom du rôle proxmox a appliquer sur les pools (defaut "etudiant")
- TMPFILE : Fichier temporaire utilisé par le script pour les étudiants (defaut "/tmp/etudiants")
- PREFIX : Préfixe à aplliquer sur les pool étudiants créés (defaut "etudiant-")
- RMPREFIX : Préfixe à appliquer sur les anciens pools (defaut "removed-")


### delete-etudiants-pool
Ce script permet de supprimer les pools marqué comme supprimés ainsi que les VMs associés.

Par défaut ce script se base sur le nom des pools commençant par "removed-".
Vous pouvez modifier la variable "RMPREFIX" du script pour modifier le préfixe des pools à supprimer.


## Fichiers

### Fichier "Gestion VMs.ods"
Ce fichier permet de gérer la répartition des VMs sur les noeuds et d'avoir une estimation des ressources utilisées et restantes.
