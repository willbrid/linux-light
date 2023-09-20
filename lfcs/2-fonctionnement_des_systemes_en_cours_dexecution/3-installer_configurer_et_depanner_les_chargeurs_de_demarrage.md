# Installer, configurer et dépanner les chargeurs de démarrage

Un chargeur de démarrage est une application permettant de charger le noyau Linux avec des paramètres facultatifs, comme les configurations de niveau d'exécution. Il peut être utilisé pour gérer différents noyaux ou le même noyau avec différentes options. Il peut également être utilisé pour gérer plusieurs systèmes d’exploitation sur une seule machine.
<br>
**GRUB2** (**GRand Unified Bootloader 2**) est le chargeur de démarrage installé sur les distributions les plus courantes disponibles. Le **/boot/grub/grub.cfg** (Ubuntu/Debian) ou **/boot/grub2/grub.cfg** (RedHat/CentOS) est la configuration et **/etc/grub.d/** contient les scripts de menu.

```
# Ubuntu/Debian
cat /boot/grub/grub.cfg
```

```
# RedHat/CentOS
cat /boot/grub2/grub.cfg
```

```
cd /etc/grub.d
ls -alhF
cat 05_debian_theme
cat 40_custom
```

Le fichier **/etc/default/GRUB** contient les paramètres qui contrôlent le comportement réel du menu GRUB. En utilisant ce fichier, nous pouvons mettre à jour des lignes de configuration telles que le délai d'attente GRUB, le style du menu, la ligne de commande par défaut...
<br><br>
Chaque fois que nous apportons des modifications à la configuration de GRUB, nous devons d'exécuter la commande **update-grub**.

```
sudo update-grub
```