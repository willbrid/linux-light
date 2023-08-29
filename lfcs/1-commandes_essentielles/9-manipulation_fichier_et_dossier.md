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