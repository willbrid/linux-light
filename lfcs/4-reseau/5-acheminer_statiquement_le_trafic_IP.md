# Acheminer statiquement le trafic IP

Parfois, il est nécessaire de contrôler le chemin emprunté par une requête réseau. En tant qu'administrateur système Linux, nous devons peut-être créer des routes statiques pour gérer le trafic réseau. <br>
Un réseau est une autoroute conçue pour acheminer les paquets d’informations vers leur destination. Parfois, un administrateur Linux doit fermer une route en raison de problèmes ou de travaux.

- Affichons la configuration réseau de notre serveur

```
ip addr show
```

- Affichons la table de routage de notre serveur

```
ip route show
```

- Installons et utilisons la commande **traceroute** pour voir comment cette machine accède à l'un des serveurs DNS de Google **8.8.0.0**

Sous Ubuntu

```
sudo apt install traceroute
```

Sous Rocky linux

```
sudo dnf install traceroute
```

Exécution de la commande

```
traceroute 8.8.0.0
```

Dans le résultat de cette commande, le premier saut est mon routeur par défaut. Ensuite, le paquet effectue plusieurs sauts. Pour certains sauts, leur périphérique n'est pas configuré pour envoyer une réponse : c'est pour nous avons des étoiles à la place. Après plusieurs sauts, nous atteignons enfin le serveur DNS de Google. Chacun de ces sauts doit généralement avoir des routes configurées pour leur dire quoi faire avec les paquets à mesure qu'ils arrivent.

- Forçons notre serveur **ubuntu-server** à utiliser notre serveur **rocky-server** comme passerelle

Activons le routage sur notre serveur **rocky-server**

```
sudo su
echo 1 > /proc/sys/net/ipv4/ip_forward
exit
```

```
sudo sysctl -p
```

Vérifions si la configuration a été appliquée

```
sudo sysctl net.ipv4.ip_forward
```

Ajoutons une route sur notre serveur **ubuntu-server** afin d'atteindre le DNS Google en passant par notre serveur **rocky-server**

```
sudo ip route add 8.8.0.0/16 proto static metric 10 via inet 192.168.56.110 dev enp0s8
```

Si nous consultons la table de routage du serveur **ubuntu-server** nous verrons qu'une route a été ajoutée

```
ip route show
```

Si nous exécutons la commande **traceroute** sur le DNS Google **8.8.0.0** sur le serveur **ubuntu-server**, nous constaterons qu'il existe un saut pointant sur le serveur **rocky-server**

```
traceroute 8.8.0.0
```

Supprimons la route nouvellement créée sur le serveur **ubuntu-server**, nous exécutons la commande

```
sudo ip route del 8.8.0.0/16 proto static metric 10 via inet 192.168.56.110 dev enp0s8
```

Si nous consultons la table de routage du serveur **ubuntu-server** nous verrons que la route a été supprimée

```
ip route show
```