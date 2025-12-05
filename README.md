# SIO Proxmox
Ce dépôt contient certains scripts et fichiers utiles pour l'administration des infrastructures Proxmox de BTS SIO de Centre Val de Loir.



## Scripts

### sync-etudiants-pool
Ce script permet la création de pools personnels pour les nouveaux étudiants membres du groupe proxmox dédié aux étudiant. Il marque également les pools des membres qui n'existent plus dans le groupe comme supprimés.

Par défaut le script crée des pools commençant par « etudiant- » et se base sur le groupe « proxmox-etudiant ». Il renomme les pools étudiants obsolètes avec le préfixe "removed-".
Vous pouvez modifier les variables du script pour changer son comportement :
- REALM : Nom du royaume proxmox (Active Directory) dont est issu le groupe étudiant (défaut "adsio")
- GROUP : Nom du groupe étudiant dans l'Active Directory (défaut "proxmox-etudiant")
- ROLE : Nom du rôle proxmox a appliquer sur les pools (defaut "etudiant")
- TMPFILE : Fichier temporaire utilisé par le script pour les étudiants (defaut "/tmp/etudiants")
- PREFIX : Préfixe à aplliquer sur les pool étudiants créés (defaut "etudiant-")
- RMPREFIX : Préfixe à appliquer sur les anciens pools (defaut "removed-")


### sync-groupes-pool
Ce script permet la création de pools de groupes pour les nouveaux groupes proxmox importés. Il marque également les pools des groupes qui n'existent plus.

Par défaut le script crée des pools commençant par « groupe- » et se base sur les groupes commençant par « proxmox- ». Il renomme les de groupes obsolètes avec le préfixe "removed-".
Vous pouvez modifier les variables du script pour changer son comportement :
- REALM : Nom du royaume proxmox (Active Directory) dont est issu le groupe étudiant (défaut "adsio")
- ADGROUP : Préfixe des groupe de l'Active Directory (défaut "proxmox-")
- ROLE : Nom du rôle proxmox a appliquer sur les pools (defaut "etudiant")
- TMPFILE : Fichier temporaire utilisé par le script pour les groupes (defaut "/tmp/groupes")
- PREFIX : Préfixe à aplliquer sur les pool de groupe créés (defaut "groupe-")
- RMPREFIX : Préfixe à appliquer sur les anciens pools (defaut "removed-")


### delete-etudiants-pool
Ce script permet de supprimer les pools marqué comme supprimés ainsi que les VMs associés.

Par défaut ce script se base sur le nom des pools commençant par "removed-".
Vous pouvez modifier la variable "RMPREFIX" du script pour modifier le préfixe des pools à supprimer.



## Services

### ha-inet
Ce service permet de surveiller une interface réseau et de passer un noeud en mode maintenance si l'interface devient down.

Mise en place du service :
- Copiez le fichier ha-inet.default dans /etc/default/ha-inet et définissez l'interface à surveiller dans le paramètre IFACE.
- Copiez le fichier ha-inet dans /sbin/ha-inet et rendez le fichier exécutable avec `chmox +x /sbin/ha-inet`
- Copiez le fichier ha-inet.service dans /etc/systemd/system/ha-inet.service
- Rechargez les services avec `systemctl daemon-reload`
- Activez le service au démarrage avec `systemctl enable ha-inet`
- Lancez le service avec `systemctl start ha-inet`


## Fichiers

### Fichier "Gestion VMs.ods"
Ce fichier permet de gérer la répartition des VMs sur les noeuds et d'avoir une estimation des ressources utilisées et restantes.
