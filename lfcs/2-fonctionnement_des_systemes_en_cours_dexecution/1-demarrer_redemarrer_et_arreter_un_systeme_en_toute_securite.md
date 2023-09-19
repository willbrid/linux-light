# Démarrer, redémarrer et arrêter un système en toute sécurité

Une machine Linux nécessite une maintenance pour les mises à jour du matériel et du système d'exploitation. Comment arrêter ou redémarrer la machine ?

### shutdown

Il s’agit de la commande incontournable pour arrêter, mettre hors tension ou redémarrer une machine. Il fonctionne sur les systèmes d'exploitation basés sur System 5 et systemd.

- **shutdown -r <TIME>** : Redémarre le serveur à l'heure spécifiée
- **shutdown -H <TIME>** : Arrête toutes les activités du processeur à l'heure spécifiée.
- **shutdown -P <TIME>** : Arrête le système d'exploitation et envoie une commande pour éteindre la machine à l'heure spécifiée.

```
shutdown -r +2
```

```
shutdown -H +5
```

```
shutdown -P +7
```

### reboot

Cette commande remplit la même fonction que **shutdown -r** , mais peut également être utilisé pour arrêter ou mettre hors tension le serveur lorsque les paramètres corrects sont envoyés.

```
reboot
```

### halt

Cette commande remplit la même fonction que **shutdown -H** et peut également être utilisé pour redémarrer ou mettre hors tension le serveur lorsque les paramètres corrects sont envoyés.

```
halt
```

### poweroff

Cette commande remplit la même fonction que **shutdown -P** et peut également être utilisé pour redémarrer ou arrêter le serveur lorsque les paramètres corrects sont envoyés.

```
poweroff
```