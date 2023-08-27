# Utiliser la redirection entrée-sortie

### Descripteurs de fichiers

- **stdin (0)** - standard input -> entrée standard
--- Comment les données sont saisies ou présentées pour le traitement <br>
--- Généralement le clavier ou la souris, mais il peut également s'agir d'un fichier

- **stdout (1)** - standard output -> sortie standard
--- Les données renvoyées par une commande

- **stderr (2)** - standard error -> erreur standard
--- Messages d'erreur renvoyés, séparés de la sortie standard

### Opérateurs de redirection

- **| (pipe)**

La commande **pipe** est utilisée pour envoyer la sortie d'une commande à une autre commande pour traitement.

```
cat /var/log/syslog | less
```

- **> (créer / écraser)**

Utilisé pour écrire la sortie d'une commande dans un fichier. Créera un fichier s'il n'existe pas, ou écrasera un fichier existant.

```
ls - l /etc > etc.txt
```

- **>> (créer / ajouter)**

Utilisé pour ajouter la sortie d'une commande à un fichier. Créera un fichier s'il n'existe pas, ou ajoutera une sortie à un fichier existant.

```
ls - l /var >> etc.txt
```

- **< (entrée)**

Utilisé pour diriger le contenu d'un fichier vers une commande. Souvent utilisé pour envoyer des données à un script pour traitement, mais également avec des commandes.

```
less < etc.txt
```