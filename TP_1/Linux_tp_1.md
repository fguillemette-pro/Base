# TP 01 - Linux
## Prérequis
Pour la réalisation de ce TP, il vous faut un client SSH:
* [Putty](https://www.putty.org/)
* [mRemote](https://mremoteng.org/download)

Assurez-vous d'avoir une connexion à internet non filtrée (dans le cas ou vous faites le TP depuis le poste de votre client)

## Initalisation

Pour vous connecter sur votre machine, il vous faut 3 élements:

* Le nom de la machine (hostname)
* Le nom d'utilisateur (login)
* Le mot de passe (password)

Il est possible, en fonction du client SSH que vous utilisez, que le numéros de port vous soit demandé. Par défaut, le service SSH s'execute sur le port 22.

Exemple avec Putty:

![Image 1](https://github.com/fguillemette-pro/Formation-Linux/blob/2e99f727c68cc41d0d9a9bfb86e1c3b855d4fe43/TP_1/img/img1.png?raw=true)

![Image 2](https://github.com/fguillemette-pro/Formation-Linux/blob/2e99f727c68cc41d0d9a9bfb86e1c3b855d4fe43/TP_1/img/img2.png?raw=true)

⚡ Les informations de connexions vous seront transmis le jour de la fomation.

## Welcome to the machine

Par défaut, le répertoire utilisé sera votre *home*.

Le *home* est votre espace personnel. Il se situe dans:
```
/home/[votre login]
```

Pour connaitre votre emplacement dans l'arborescence, tapez la commande suivante:

```
pwd
```

> **pwd** affiche votre répertoire courant ou répertoire de travail (path working directory) 

Pour lister les fichiers, tapez la commande:
```
ls
```

Cette commande peut se combiner avec des options comme -a, comme ceci:
```
ls -al
```
> La commande **ls -al** affiche les fichiers et dossiers **cachés** et **des informations supplémentaires** dans le répertoire courant

Vous pouvez préciser le répertoire ou la commande s'execute, par exemple:

```
ls -al /etc/
```
> La commande **ls** s'execute dans le répertoire **/etc/** avec **les options -al**


Pour retrouver toutes les options possibles, vous pouvez utiliser cette commande avec man:

```
man ls
```
Pour quitter le manuel, tapez **q**.

La commande **man** fonctionne avec toutes les autres commandes du système, abusez de cette commande, elle sera la meilleur source de vérité à votre disposition !

Pour vous déplacer dans l'arborescence, utiliser la commande:
```
cd [votre chemin]
``` 

Exemple:

```
cd /etc/
```

Si vous faites un **pwd**, vous n'êtes plus dans votre *home*.

