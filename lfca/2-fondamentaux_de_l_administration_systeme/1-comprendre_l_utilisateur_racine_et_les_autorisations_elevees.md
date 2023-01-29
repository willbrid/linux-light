# Comprendre l'utilisateur racine et les autorisations élevées

## Définition

- **utilisateur root** : le compte root est un compte d'utilisateur spécial utilisé pour l'administration sur l'hôte Linux. Contrairement aux autres utilisateurs, l'utilisateur root a accès à tous les fichiers et programmes et a la possibilité de changer la propriété, les autorisations et de modifier les comptes d'utilisateurs (entre autres). Le compte root est également appelé **superutilisateur**, **administrateur** et parfois **admin** en abrégé.

- **/etc/sudoers** : il est utilisé pour déterminer les privilèges **sudo** d'un utilisateur ou d'un groupe. Les fichiers du répertoire, **/etc/sudoers.d**, sont lus avec le fichier **sudoers** pour déterminer les privilèges. Ce répertoire, comme d'autres, est utilisé pour faciliter l'organisation et l'ordre des configurations.

- **/etc/ssh/sshd_config** : c'est le fichier de configuration du démon ssh openssh. Afin de désactiver les connexions root à distance, il faudrait définir l'option **PermitRootLogin** sur **no** (l'option doit être décommentée). Pour appliquer les modifications, il faudrait redémarrer le service **sshd**.

- **visudo** : il est utilisé pour éditer le fichier sudoers. Il fournit un verrou sur le fichier sudoers contre plusieurs modifications simultanées, fournit des vérifications de base et vérifie les erreurs d'analyse. Différents éditeurs peuvent être utilisés avec visudo, mais il utilise **vi** par défaut.

- **su** (**switch user** ou **substitute user**) : il permet à l'utilisateur d'exécuter un interpréteur de commandes en changeant d'**identifiant de groupe** (**GID**) et d'**identifiant d'utilisateur** (**UID**). Lorsqu'il est exécuté sans arguments, il exécute par défaut un shell interactif en tant qu'utilisateur **root** (c'est à dire la commande utilise les UID **0** et le GID **0** qui sont ceux du compte utilisateur root). Les options **-**, **-l** et **--login** lanceront le shell comme un shell de connexion avec un environnement similaire à une connexion réelle. La commande **su** démarre un interpréteur de commandes à l'intérieur de la nouvelle session utilisateur.

- **sudo** : il permet à l'utilisateur d'exécuter une commande en tant que superutilisateur (**root**) ou un autre utilisateur (à l'aide de l'option **-u**). L'option -i (ou --login) exécutera le shell interactif si aucune commande n'est spécifiée. Les privilèges **sudo** sont définis dans le fichier sudoers.

## Pratiques

- Désactivons les connexions root à distance par ssh

```
sudo vim /etc/ssh/sshd_config
```

```
---
PermitRootLogin no
---
```

```
sudo systemctl restart sshd
```

Si nous essayons de nous connecter par ssh avec l'utilisateur **root**, ça ne marchera pas.

- ouvrir un interpréteur de commandes en tant que root

```
sudo su -
```

ou

```
sudo -i
```

- étudions le fichier **/etc/sudoers** avec ces 3 lignes ci-dessous

```
rodrigue    ALL=(ALL)       ALL
%wheel  ALL=(ALL)       ALL
includedir /etc/sudoers.d
```

Maintenant, nous pouvons voir quelques distinctions : <br>
--- lorsque nous utilisons un nom d'utilisateur, nous tapons simplement ce nom d'utilisateur <br>
--- si nous souhaiterons associer à un groupe, nous devons ajouter ce signe **%** devant le nom du groupe. Et cela permet au système de savoir qu'il s'agira d'un groupe. <br>
--- nous avons plusieurs fois le mot clé **ALL** : <br>
------- Le premier **ALL**, va représenter l'hôte sur lequel ils peuvent l'exécuter. Et **ALL** signifie sur n'importe quel hôte. <br>
------- Et puis le suivant **ALL**, qui est entre parenthèses ici, va être l'utilisateur ou le groupe pour l'exécuter. <br>
------- Et puis le dernier **ALL** que nous voyons ici, va être les commandes. <br>
