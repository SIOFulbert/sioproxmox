# SIO Proxmox
Ce dépôt contient certains scripts et fichiers utiles pour l'administration des infrastructures Proxmox de BTS SIO de Centre Val de Loir.



## Scripts

### cluster-maintenance enable|disable
Ce script permet l'entrée en mode maintenance de tout les noeuds du cluster avec le paramètre "enable". Cela est utile pour permettre l'extinction totale du cluster.
La sortie du mode maintenance de tous les noeuds est réalisé avec le paramètre "disable".


### sync-iso IDSTOCKAGE
Ce script permet d'envoyer les images ISO présentes dans le stockage IDSTOCKAGE vers les autres noeuds du cluster.


### sync-personal-pool [groupe]
Ce script permet la création de pools personnels pour les nouveaux membres du groupe spécifié et commençant par « proxmox- » (le préfixe « proxmox- » n'est pas à spécifier dans le pamrètre). Il marque également les pools des membres qui n'existent plus dans le groupe comme supprimés.

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


### delete-removed-pool
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

Il est possible de se passer du service et d'utiliser directement la commande pour lancer une vérification :

`ha-inet [interface]`

Si aucun paramètre n'est passé, c'est l'interface renseignée dans le fichier /etc/default qui sera prise en compte.

## Fichiers

### Fichier "Gestion VMs.ods"
Ce fichier permet de gérer la répartition des VMs sur les noeuds et d'avoir une estimation des ressources utilisées et restantes.
