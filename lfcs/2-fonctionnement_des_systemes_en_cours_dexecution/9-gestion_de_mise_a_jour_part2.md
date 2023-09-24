# Mettre à jour et gérer les logiciels pour fournir les fonctionnalités et la sécurité requises, partie 2 - CentOS/Redhat

En tant qu'administrateur système, maintenir la stabilité et la sécurité est une tâche essentielle. Les mises à jour du système et les correctifs constituent un élément clé de cet objectif.
<br><br>
Les distributions **Redhat/CentOS** offrent plusieurs outils pour maintenir le système d'exploitation et les applications à jour afin de maintenir la santé du système.

### rpm

- Gestionnaire de packages pour les systèmes basés sur RedHat
- Outil de bas niveau utilisé pour installer, supprimer et fournir des informations sur les packages RPM téléchargés
- Répertorie manuellement les dépendances des packages, effectue des vérifications de dépendances mais n'installe pas automatiquement
- Syntaxe :

```
# Installation d'un package
rpm -ivh filename.rpm

# Mise à niveau d'un package
rpm -Uvh filename.rpm

# Suppression d'un package
rpm -e pkgname

# Lister les packages installés
rpm -qa

# Obtenir les informations sur un package
rpm -qi pkgname

# Trouver le propriétaire du fichier
rpm -qf /path/to/file
```

Exemples : <br>

Lister les packages installés
```
rpm -qa
```

Lister les packages associés à **ssh**
```
rpm -qa | grep ssh
```

Trouver le package associé au fichier binaire **/usr/bin/gzip**
```
rpm -qf /usr/bin/gzip
```

Afficher les informations sur le package **gzip**
```
rpm -qi gzip
```

### yum

- Gestionnaire de packages pour les systèmes RedHat
- Outil officiel de haut niveau qui fournit une interface de ligne de commande pour installer, mettre à niveau, supprimer et fournir des informations sur les packages **.rpm**
- Gère les contrôles de dépendance
- Syntaxe :

```
# Installation d'un package
yum install pkgname

# Suppression d'un package
yum remove pkgname

# Mise à jour d'un package
yum update pkgname

# Lister les packages installés
yum list installed

# Rechercher dans les référentiels un package
yum search keyword
```

Exemples : <br>

Lister les packages installés
```
yum list installed
```

Lister les packages associés à **ssh**
```
yum list installed | grep ssh
```

Rechercher dans les référentiels le package tmux
```
yum search tmux
```

Installer le package tmux
```
sudo yum install tmux
```

Désinstaller le package tmux
```
sudo yum remove tmux
```

Rechercher les packages à mettre à jour
```
yum check-update
```

Mettre à jour un package
```
sudo yum update python-perf.x86_64
```

### dnf

- Outil de haut niveau qui fournit une interface de ligne de commande pour installer, mettre à niveau, supprimer et fournir des informations sur les packages **.rpm**
- Gère les contrôles de dépendance
- Gestionnaire de paquets par défaut pour **Fedora** et **RedHat8**. Conçu pour de meilleures performances, une optimisation de la mémoire et une résolution améliorée des dépendances
- Partage de nombreuses commandes et similitudes avec yum
- Syntaxe :

```
# Installation d'un package
dnf install pkgname

# Suppression d'un package
dnf remove pkgname

# Mise à jour d'un package
dnf update pkgname

# Lister les packages installés
dnf list installed

# Rechercher dans les référentiels un package
dnf search keyword
```

Exemples : <br>

Lister les packages installés
```
dnf list installed
```

Installer le package tmux
```
sudo dnf install tmux
```

Désinstaller le package tmux
```
sudo dnf remove tmux
```