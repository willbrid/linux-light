# Gestion des utilisateurs et des groupes

## Définition

- **useradd** : créer un nouvel utilisateur ou mettre à jour les informations par défaut du nouvel utilisateur.

- **groupadd** : créer un nouvel groupe.

- **usermod** : modifie un compte d'utilisateur.

- **groupmod** : modifie une définition de groupe sur le système

- **userdel** : supprimer un compte utilisateur et ses fichiers associés

- **groupdel** : supprimer un groupe

- **passwd** : modifier un mot de passe utilisateur. Le super utilisateur root, peut changer le mot de passe de n'importe quel utilisateur.

## Pratiques

- Connectons nous avec le compte root

```
sudo -i
```

- créons un groupe appelé **dev** 

```
groupadd dev
```

- vérifions que le groupe **dev** a bien été créé

```
cat /et/group
cat /et/group | grep dev
```

- créons un groupe en définissant son identifiant

```
groupadd -g 1500 ops
```

- créons un utilisateur **willbrid**

```
useradd willbrid
```

Cette commande créera aussi un répertoire **willbrid** dans le répertoire **home**.

```
ls /home
```

- affichons les identifiants d'utilisateur et de groupe réels et effectifs pour l'utilisateur **willbrid**

```
id willbrid
```

--- **uid** : identificant de l'utilisateur **willbrid** <br>
--- **gid** : identifiant du groupe par défaut de l'utilisateur **willbrid** <br>
--- **groups** : identifiants des autres groupes de l'utilisateur **willbrid** <br>

Sans argument la commande id permet d'afficher ces informations pour l'utilisateur courant.

- créons un utilisateur **rodrigue** sans son repertoire personnel avec son groupe par défaut **ops**

```
useradd -M -g ops rodrigue
```

L'option **-M** permet d'éviter de créer le répertoire personnel et l'option **-g** permet de préciser le groupe par défaut.

- listons tous les utilisateurs du système

```
cat /etc/passwd
```

- modifions l'identifiant de l'utilisateur **willbrid** et ajoutons le dans les groupes : dev et ops

```
usermod -G dev,ops -u 1700 willbrid
```

L'option **-G** permet de préciser les groupes (séparés par la virgule) où l'utilisateur sera attribué et l'option **-u** permet de mettre à jour l'identifiant de l'utilisateur **willbrid**

- mettons à jour le nom du groupe **dev** en **dev2**

```
groupmod -n dev2 dev
```

- creons un répertoire **/home/flash** et définissons le comme répertoire personnel de l'utilisateur **rodrigue**

```
mkdir /home/flash
chown rodrigue:ops /home/flash/
usermod -d /home/flash/ rodrigue 
```

L'option **-d** permet de modifier le répertoire personnel de l'utilisateur **rodrigue**.
<br>
En affichant le contenu du fichier **/etc/passwd**, on aura à la dernière ligne :

```
rodrigue:x:1003:1500::/home/flash/:/bin/bash
```

- supprimons le goupe **dev2**

```
groupdel dev2
```

- supprimons l'utilisateur **willbrid**

```
userdel willbrid
```

- mettons à jour le mot de passe de l'utilisateur **rodrigue**

```
passwd rodrigue
```

- connectons nous avec le nouveau mot de passe avec l'utilisateur **rodrigue**

```
exit
su - rodrigue
```

La commande **su** permet d'exécuter des commandes avec un utilisateur et un ID de groupe de substitution. L'option **-** (**-l**, **-login**) permet de démarrer le shell en tant que shell de connexion avec un environnement similaire à une connexion réelle : 
<br>
--- efface toutes les variables d'environnement sauf **TERM** <br>
--- initialise les variables d'environnement **HOME**, **SHELL**, **USER**, **LOGNAME** et **PATH** <br>
--- modifications apportées au répertoire personnel de l'utilisateur cible <br>
--- définit **argv[0]** du shell sur **'-'** afin de faire du shell un shell de connexion
