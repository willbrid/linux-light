# Mettre à jour et gérer les logiciels pour fournir les fonctionnalités et la sécurité requises, partie 1 - Ubuntu/Debian

En tant qu'administrateur système, maintenir la stabilité et la sécurité est une tâche essentielle. Les mises à jour du système et les correctifs constituent un élément clé de cet objectif.
<br><br>
Les distributions **Debian/Ubuntu** offrent plusieurs outils pour maintenir le système d'exploitation et les applications à jour, afin de maintenir la santé du système.

### dpkg

- Gestionnaire de paquets pour les systèmes basés sur Debian
- Outil de bas niveau utilisé pour installer, supprimer et fournir des informations sur les packages **.deb** téléchargés
- N'effectue pas de contrôles de dépendance
- Syntaxe :

```
# Installation d'un package
dpkg -i filename.deb
# Liste des paquets installés
dpkg -l
# Désinstallation d'un package
dpkg -r pkgname
```

Vérifier si les commandes **zip** et **unzip** sont installées

```
dpkg -l zip
```

```
dpkg -l unzip
```

### aptitude

- Interface de haut niveau avec le système de paquets Debian
- Fournit une interface frontale en ligne de commande pour installer, mettre à niveau, supprimer et fournir des informations sur les packages **.deb**
- Gère les contrôles de dépendance
- Peut être utilisé avec les options de ligne de commande mais plus couramment utilisé pour son interface
- Syntaxe :

```
# Installation d'un package
aptitude install pkgname

# Liste des informations sur un package
aptitude show pkgname

# Désinstallation d'un package
aptitude remove pkgname
```

Pour afficher l'interface interactive, on exécute :

```
sudo aptitude
```

### apt/apt-get

- Interface de haut niveau avec le système de paquets Debian
- Fournit une interface de ligne de commande pour installer, mettre à niveau, supprimer et fournir des informations sur les packages **.deb**
- Gère les contrôles de dépendance
- Syntaxe :

```
# Installation d'un package
apt install pkgname

# Liste des informations sur un package
apt -cache show pkgname

# Désinstallation d'un package
apt purge pkgname
```

|        apt       | apt-get                   | description                                                            |
| :---             | :----:                    | ---:                                                                   |
| apt install      | apt-get install           | installer un package                                                   |
| apt remove       | apt-get remove            | désinstaller un package                                                |
| apt purge        | apt-get purge             | désinstaller un package avec ses configurations                        |
| apt update       | apt-get update            | actualiser l'index du référentiel                                      |
| apt upgrade      | apt-get upgrade           | effectuer les mises à niveau                                           |
| apt autoremove   | apt-get autoremove        | supprimer les packages indésirables                                    |
| apt full-upgrade | apt-get dist-upgrade      | mettre à niveau les packages avec gestion automatique des dépendances  |
| apt search       | apt-cache search          | rechercher un programme                                                |
| apt show         | apt-cache show            | afficher les détails d'un package                                      |


```
sudo apt update
```

```
apt search htop
```

```
apt search tmux
```

```
sudo apt install tmux
```

```
sudo apt remove tmux
```