# Rechercher des fichiers [Part1]

Pour débuter créeons 4 fichiers et déplaçons les dans le répertoire **/etc**

```
cd ~/
touch search.txt && touch SeArch.txt && touch SeARCH.txt && touch SEARCH.txt
sudo mv search.txt /etc/
sudo mv SeArch.txt /etc/
sudo mv SeARCH.txt /etc/
sudo mv SEARCH.txt /etc/
```

## Commande find

--- Commande très puissante utilisée pour rechercher des fichiers ou des répertoires <br>
--- Peut rechercher par nom, type de fichier, horodatage et de nombreux autres attributs de fichier <br>
--- Prend en charge les expressions et les blobs pour les recherches avancées <br>
--- Recherche en temps réel, ce qui peut être lent sur les machines avec beaucoup de fichiers <br>

- **Recherche de fichiers par son nom dans le répertoire courant**

```
find -name "search.txt"
```

- **Recherche de fichiers par son nom dans tout le système**

```
find / -name "search.txt"
```

En mode non privilège, nous constaterons plusieurs lignes d'erreur mentionnant que nous n'avons pas de permission.

```
sudo find / -name "search.txt"
```

- **Recherche de fichiers par son nom dans un repertoire spécifique**

```
sudo find /etc -name "search.txt"
```

- **Recherche de fichiers par son nom dans un repertoire spécifique sans respecter la casse sur le nom du fichier**

```
sudo find /etc -iname "search.txt"
```

- **Recherche de fichiers par son type et par son nom dans tout le système**

```
sudo find / -type f -name "*.log"
```

Les types de fichiers sont : <br>
--- **b** -> bloc (tamponné) spécial <br>
--- **c** -> caractère (non tamponné) spécial <br>
--- **d** -> répertoire <br>
--- **p** -> tube nommé (FIFO) <br>
--- **f** -> fichier régulier <br>
--- **l** -> lien symbolique : ceci n'est jamais vrai si l'option **-L** ou l'option **-follow** est active, sauf si le lien symbolique est rompu. Si nous souhaitons rechercher des liens symboliques lorsque **-L** est activé, utiliseons **-xtype**. <br>
--- **s** -> socket <br>
--- **D** -> door (Solaris) <br>

Pour rechercher plusieurs types à la fois, nous pouvons fournir la liste combinée des lettres de type séparées par une virgule `,' (extension GNU).

- **Recherche de fichiers par son type et par le nom de son propriétaire dans un repertoire spécifique**

```
sudo find /etc -type f -user username
```

**username** est le nom d'utilisateur avec lequel on est connecté sur le système.

## Commande locate

--- Recherche plus rapide que la commande **find** <br>
--- Options de recherche limitées : impossible de rechercher par attributs ou métadonnées <br>
--- Recherche par défaut sur le système de fichiers complet <br>
--- S'appuie sur une base de données pour la recherche, qui doit être rafraîchie régulièrement <br>
--- Par défaut la recherche est faite en respectant la casse

- **Recherche de fichiers par son nom**

```
locate "search.txt"
```

Nous pouvons mettre à jour la base de données de recherche de la commande **locate**.

```
sudo updatedb
```

Recherchons à nouveau notre fichier **search.txt** et nous aurons plusieurs résultats.

- **Recherche de fichiers par son nom sans respecter la casse sur ce nom**

```
locate -i "search.txt"
```