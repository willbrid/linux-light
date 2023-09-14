# Gérer l'accès au compte root

Le compte root a accès pour gérer et modifier l'ensemble du système. Pour sécuriser et protéger le système, comment restreindre l'accès au root ?

### Comment éviter le root

Connectons-nous toujours en tant que nous-même ou en utilisant un autre compte non privilégié !
- **sudo - superuser do** : accorde des privilèges élevés temporaires pour exécuter une commande
- **su - substitute user** : modifications apportées au compte root jusqu'à la déconnexion

### Comment gérer l'accès sudo

- L'accès est accordé via les entrées du fichier **/etc/sudoers**
- L'accès peut être géré par compte ou par groupe
<br>
- Commande **whoami** : Imprime le nom d'utilisateur associé à l'ID utilisateur effectif actuel.

```
whoami
```

Il est équivalent à la commande

```
id -un
```

- Commande **id** : imprime les informations sur l'utilisateur et le groupe pour l'utilisateur spécifié ou (lorsque l'utilisateur est omis) pour l'utilisateur actuel.

```
id root
```

```
id
```

- Affichons le contenu du fichier **/etc/sudoers**

```
sudo cat /etc/sudoers
```

- Section de spécification des privilèges utilisateur

```
root	ALL=(ALL:ALL) ALL
```

En règle générale, c'est ici que nous entrons les comptes d'utilisateurs individuels pour leur accorder l'accès. Dans ce fichier sudoers particulier, seul le compte root a obtenu l'accès individuellement et les privilèges qui ont été accordés à root nous définissent : <br>
--- le premier **ALL** indique que le compte root peut s'exécuter à partir de n'importe quelle session de terminal. <br>
--- la section suivante, entre parenthèses (**ALL:ALL**), indique que le compte root peut s'exécuter avec tous les utilisateurs et tous les groupes. <br>
--- et le **ALL** final signifie que l'utilisateur root peut exécuter n'importe quelle commande.

- Section des membres du groupe d'administrateurs (**admin**) qui peuvent obtenir les privilèges root

```
%admin ALL=(ALL) ALL
```

Nous pouvons voir que le groupe **admin** a obtenu des autorisations et ici nous pouvons voir que le groupe sudo a obtenu des autorisations.

- Section autorisant les membres du groupe **sudo** à exécuter n'importe quelle commande

```
%sudo	ALL=(ALL:ALL) ALL
```

Créeons un utilisateur **basicuser** avec un mot de passe **test**

```
sudo adduser basicuser
```

Connectons nous avec l'utilisateur **basicuser** depuis notre utilisateur courant ayant les privilèges **sudo**

```
su basicuser
```

Une fois connecté, en exécutant les commandes ci-dessous.

```
cat /etc/sudoers
```

Ici, nous pouvons constater que nous n'avons pas les droits avec cet utilisateur.

```
sudo cat /etc/sudoers
```

Ici, Un message d'erreur s'affiche indiquant l'absence de l'utilisateur **basicuser** dans le fichier **/etc/sudoers**.
<br>

Déconnectons nous de la session de l'utilisateur **basicuser**

```
exit
```

Donnons les droits **sudo** à l'utilisateur **basicuser**

```
sudo visudo
```

```
...
# User privilege specification
...
basicuser   ALL=(ALL:ALL) ALL
...
```

Reconnectons nous à nouveau au compte d'utilisateur **basicuser** et affchons le contenu du fichier **/etc/sudoers** avec **sudo**

```
su basicuser
```

```
sudo cat /etc/sudoers
```

Nous constatons que le contenu du fichier s'affiche.
<br>

Déconnectons nous de la session de l'utilisateur **basicuser**

```
exit
```

Ajoutons l'utilisateur **basicuser** au groupe **sudo** présent dans le fichier **/etc/sudoers**

```
sudo gpasswd -a basicuser sudo
```

La commande **gpasswd** est utilisée pour administrer **/etc/group** et **/etc/gshadow**. Chaque groupe peut avoir des administrateurs, des membres et un mot de passe. <br>
Nous pouvons vérifier que l'utilisateur appartient désormais au groupe **sudo** en exécutant la commande

```
id basicuser
```

Si nous nous connectons à nouveau au compte **basicuser** et nous exécutons avec **sudo** la commande affichant le contenu du fichier **/etc/sudoers**, nous constaterons que le contenu du fichier s'affiche car nous appartenons désormais au groupe **sudo**.
<br>

Enlevons l'utilisateur **basicuser** au groupe **sudo**

```
sudo gpasswd -d basicuser sudo
```
