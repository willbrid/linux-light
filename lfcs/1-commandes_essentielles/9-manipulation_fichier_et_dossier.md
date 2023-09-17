# Créer, supprimer, copier et déplacer des fichiers et des répertoires

### Créer un fichier 

```
cd ~
```

Plusieurs façons de créer un fichier

```
touch filename1.txt
nano filename2.txt
command > filename3.txt
```

**Exemple :**

```
touch filename1.txt
nano filename2.txt # avec pour contenu : <Bonjour tout le monde>
echo "Bonjour tout le monde" > filename3.txt
```

### Copier un fichier

```
cp filename1.txt filename.txt
```

### Déplacer un fichier

```
mv filename1.txt Documents/filename1.txt
```

### Rénommer un fichier

```
mv filename.txt filename4.txt
```

### Créer un répertoire

```
mkdir path/to/directory
```

**Exemple :**

```
mkdir target1
mkdir target2
```

### Supprimer un fichier

```
rm filename4.txt
rm Documents/filename1.txt
```

### Supprimer un répertoire

- Ne fonctionne que si le répertoire est vide

```
rmdir directory
```

**Exemple :**

```
rmdir target1
```

- Supprime tous les fichiers ainsi que le répertoire

```
rm -r directory
```

**Exemple :**

```
rm -r target2
```

- Dangereux ! Supprime tous les fichiers et répertoires sans avertissement

```
rm -rf directory
```

### Transférer des fichiers en toute sécurité sur le réseau

Ici nous supposons que nous avons deux serveurs : 

- **server1**, son user **user1** et son repertoire **/opt/app**

- **server2**, son user **user2** et son repertoire **/opt/api**

Nous supposerons que nous sommes connectés par ssh sur le serveur **server1**. 
<br><br>
Utilisons **ls -lR /opt/** localement sur le serveur **server1**, puis exécutons-la à distance sur le serveur **server2** avec ssh

```
ls -lR /opt
ssh user2@server2 ls -lR /opt
```

Copions en toute sécurité le répertoire **/opt/app** du serveur **server1** vers le répertoire **/opt** sur le serveur **server2**

```
scp -rp /opt/app user2@server2:/opt
```

L'option **-r** la rend récursif et **-p** lui permet de conserver les horodatages et les autorisations.
<br><br>
Synchronisons le répertoire **/opt/api** du serveur **server2** avec le serveur **server1**

```
rsync -aP user2@server2:/opt/api /opt
```

Vérifions que les répertoires **/opt/app** et **/opt/api** sont les mêmes sur **server1** et **server2**

```
# Sur server1
ls -lR /opt
# Sur server2
ssh user2@server2 ls -lR /opt
```

Nous pouvons utiliser la commande **rsync** pour vérifier que le **contenu**, les **horodatages** et les **autorisations** sont les mêmes.

```
rsync -naP /opt/ user2@server2:/opt
```

L'option **-n** permet d'effectuer un **dry-run** sans aucune modification, l'option **-a** permet d'activer le mode archive et l'option **-P** est équivalent aux options combinées **--partial --progress** qui permettent de conserver les fichiers partiellement transférés (**--partial**) et d'afficher la progression pendant le transfert (**--progress**).