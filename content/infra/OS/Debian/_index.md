+++
title = "Iptables"
date = 2022-03-28T20:43:16+02:00
weight = 5
chapter = true
pre = ""
+++

# Iptables

Debian est une distibution linux composée de projet open sources et maintenu par l'organisation "Debian Project". Debian est une distribution "native", elle n'est issue d'aucune autre distrib, contrairement à Ubuntu qui elle est basée sur Debian.


![Archi](https://killbzz.github.io/images/archi-simple.png)

## 
23

If you have systemd in version greater than 213 (check: systemd --version), you don't have to install ntp package to synchronize system time.

systemd provides systemd-timesyncd daemon which implements SNTP (Simple NTP) client.

To start and enable SNTP synchronization:

timedatectl set-ntp true
To show current settings of the system clock and RTC:

timedatectl status

## Redirection de port 

Pour rediriger un port avec iptables, nous allons effectuer la commande suivante : 

```
iptables -t nat -A PREROUTING -i <CARTE RESEAU EXTERNE> -p tcp --dport <NUMERO DU PORT> -j DNAT --to <IP DU SERVEUR CIBLE>

```

### Exemples 

Cette commande va avoir pour effet de rediriger le traffic arrivant sur le port __8080__ sur l'interface ens33 vers le serveur 192.168.5.10 sur le port __8080__

```
iptables -t nat -A PREROUTING -i ens33 -p tcp --dport 8080 -j DNAT --to 192.168.5.10
```

Une alternative à cette commande vers être celle-ci, elle va permettre comme la précédente de rediriger le traffic arrivant sur le port __8080__ sur l'interface ens33 vers le serveur 192.168.5.10 MAIS cette fois sur le port __80__

```
iptables -t nat -A PREROUTING -i ens33 -p tcp --dport 8080 -j DNAT --to 192.168.5.10:80
```
