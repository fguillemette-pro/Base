# TP 01 - Linux
## Prérequis
Pour la réalisation de ce TP, il vous faut un client SSH:

* [Putty](https://www.putty.org/)
* [mRemote](https://mremoteng.org/download)

Assurez-vous d'avoir une connexion à internet non filtrée (dans le cas ou vous faites le TP depuis le poste de votre client)

## [K2] Initialisation

Pour vous connecter sur votre machine, il vous faut 3 éléments:

* Le nom de la machine (hostname)
* Le nom d'utilisateur (login)
* Le mot de passe (password)

Il est possible, en fonction du client SSH que vous utilisez, que le numéro de port vous soit demandé. Par défaut, le service SSH s'exécute sur le port 22.

Exemple avec Putty:
<center>

![Image 1](https://github.com/fguillemette-pro/Formation-Linux/blob/2e99f727c68cc41d0d9a9bfb86e1c3b855d4fe43/TP_1/img/img1.png?raw=true)

![Image 2](https://github.com/fguillemette-pro/Formation-Linux/blob/2e99f727c68cc41d0d9a9bfb86e1c3b855d4fe43/TP_1/img/img2.png?raw=true)

</center>

> Les informations de connexions vous seront transmises le jour de la formation.

## Welcome to the machine

### [K2,K4] L'arborescence

Par défaut, le répertoire utilisé sera votre *home*.

Le *home* est votre espace personnel. Il se situe dans:

```bash
/home/[votre login]
```

Pour connaitre votre emplacement dans l'arborescence, tapez la commande suivante:

```bash
pwd
```

> **pwd** affiche votre répertoire courant ou répertoire de travail (path working directory).

Pour lister les fichiers et les repertoires, tapez la commande:

```bash
ls
```

Cette commande peut se combiner avec des options comme -al (-a + -l), comme ceci:

```bash
ls -al
```
> La commande **ls -al** affiche les fichiers et dossiers **cachés** et **des informations supplémentaires** dans le répertoire courant.

Vous pouvez préciser le répertoire ou la commande s'execute, par exemple:

```bash
ls -al /etc/
```
> La commande **ls** s'execute dans le répertoire **/etc/** avec **les options -al**.


Pour retrouver toutes les options possibles, vous pouvez utiliser cette commande avec man:

```bash
man ls
```
Pour quitter le manuel, tapez **q**.

La commande **man** fonctionne avec toutes les autres commandes du système, abusez de cette commande, elle sera la meilleure source de vérité à votre disposition !

Pour vous déplacer dans l'arborescence, utiliser la commande:

```bash
cd [votre chemin]
``` 

Exemple:

```bash
cd /etc/
```

Si vous faites un **pwd**, vous n'êtes plus dans votre *home* mais dans */etc/*.

### Les fichiers et répertoires

Il existe de nombreux outils pour lire et éditer les fichiers sous Linux.

la commande la plus simple pour lire un fichier est la commande **cat**:

```bash
cat /chemin/du/fichier
```

Exemple:

```bash
cat /var/log/dnf.log
```

La commande **cat** affiche le contenu du fichier directement dans le terminal.

Il existe la commande **less** qui permet de "naviger" dans le fichier de manière plus simple.

```bash
less /var/log/dnf.log
```

> Pour quitter **less**, tapez **q**. 

> Pour faire des recherches dans votre fichier, tapez **/** puis **votre expression** dans **less**

Vous pouvez lire des fichiers cachés (tant que vous avez les permissions):

```bash
cat /.top_secret/primes_2022.txt
```

Pour créer un fichier, la commande **touch** sera votre amie:

```bash
touch /chemin/de/votre/fichier
```

Exemple:

```bash
touch ~/hello_world.txt
```

> Le **~** remplace le chemin de votre *home* (/home/user)

La création de répertoire est très similaire à la création de fichier:

```bash
mkdir /chemin/du/dossier
```
Exemple:
```bash
mkdir ~/nouveau_dossier
```
> Utilisez l'option -p pour créer les dossiers de votre répertoire.

### Vim

Vim est un éditeur de fichier qui à lui tout seul pourrait faire l'objet d'un cour de 6h, donc nous irons à l'essentiel.

Pour ouvrir un fichier sous vim:
```bash
vim ~/config.txt
```
Par défaut, vous êtes en lecture seul, pour éditer le fichier, tapez **i**.

Pour **enregistrer et quitter Vim**, Faites d'abord **echap**, puis tapez **:wq**.

### La suppression

Une commande bien dangereuse est la commande **rm**, elle efface dossiers et fichiers:

Pour un fichier:
```bash
rm ~/hello_world.txt
```

Pour un repertoire:
```bash
rm -r ~/nouveau_dossier
```

### La copie de fichiers et de repertoires

Pour copier un fichier, utilisez la commande **cp**:

```bash
cp /chemin/source /chemin/cible
```

> vous pouvez changer le nom du fichier en sortie pour faire une backup, exemple : cp /ma/config.txt /ma/config.txt.backup

### Le déplacement et renommer de fichiers et de repertoires

Pour déplacer et/ou renommer un fichier, utilisez la commande **mv**:

```bash
mv /chemin/source /chemin/cible
```

### Challenge me !

Mettons en pratique les commandes vues précédemment:

Q1: Dans votre *home*, faites un dossier *tp_01*

<details>
    <summary>Solution Q1</summary>
    
    mkdir ~/tp_01

</details>

---
Q2: Toujours depuis votre *home*, faites un fichier **super_config.txt** avec comme contenu **"hello world"** dans le repertoire *tp_01*

<details>
    <summary>Solution Q2</summary>
    
    touch ~/tp_01/super_config.txt
    vim ~/tp_01/super_config.txt

</details>

---

Q3: Supprimez le repertoire *tp_01* en une commande

<details>
    <summary>Solution Q3</summary>
    
    rm -r tp_01

</details>

---
## Permission denied

### Chmod

Pour cette partie, vous allez faire un fichier **config.txt** dans */tmp*

```bash
touch /tmp/config.txt
```
> Le dossier */tmp* est un repertoire temporaire qui sera vidé à chaque redémarrage de la machine.

Si vous faites un **ls -l** dans le repertoire, vous aurez ceci:
```
[etudiant@s1-2-sbg5 tmp]$ ls -l
total 0
-rw-rw-r--. 1 etudiant etudiant  0 Sep 19 16:31 config.txt
drwx------. 3 root     root     17 Sep 19 16:27 systemd-private-884f34e99f9949fdbd015524b4dda1b2-chronyd.service-AaqNkh
```
Votre fichier config.txt a les droits: `-rw-rw-r--`

Le propriétaire du fichier a les droits de lecture et écriture (mais pas le droit d'execution).

Le groupe du fichier a les droits de lecture et écriture (mais pas le droit d'execution).

Les autres (utilisateurs) du fichier a le droit de lecture (mais pas les droits d'écriture ou d'execution).

> Voici [un calculateur](https://chmod-calculator.com/) pour comprendre "graphiquement" le calcul.

Pour vous donnez le droit d'execution, faites la commande suivante:

```bash
chmod u+x /tmp/config.txt
```
> **u** correspond au **U**ser, **+** à **l'affectation** et **x** au droit d'**eXecution**

OU

```bash
chmod 764 /tmp/config.txt
```

Voici un résumé des droits sous Linux:

<center>

![Tableau droits linux](https://d33wubrfki0l68.cloudfront.net/794f22a6b63c1c7ad76636b195b85b3192b09f71/39aa9/assets/images/linux/lucidchart/d4e99828-d7bb-40ae-9c7e-f145c47350fc.png)

</center>

### Les utisateurs et les groupes

Pour la suite de l'exercice, je vous donne accès à trois utilisateurs:

* asterix
* obelix
* cesar

Le mot de passe est " Uderzo! " pour les trois comptes.

asterix et obelix font partie du même groupe: gaulois

cesar a son propre groupe: romain

Pour connaitre le groupe d'un d'utilisateur:

```bash
groups <user>
```
> A noter qu'un utilisateur a son propre groupe (du même nom).

Pour passer d'un utilsateur à un autre, tapez:

```bash
su <login>
```
Pour fermer la session:
```
exit
```
### Sudo

Dans le cadre de ce TP, je vous donne les droits administrateurs.

Il existe un utilitaire pour donner les droits devenir root.

> Le compte **root** est le compte administrateur sur une machine linux, nous allons voir ça dans la prochaine session.

Pour utiliser une commande qui nécéssite les droits root:
```
sudo <commande>
```
<center>

![spider advice](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSWLN0EDUm93wnBo6vB9MAwJewL0pm2MiANWw&usqp=CAU)

</center>

### Creation d'utilisateur

Dans chaque village Gaulois, il y a un chef: **abraracourcix**

```bash
sudo adduser abraracourcix
```
Si vous essayez de vous connecter sur le compte d'Abraracourcix, vous ne pouvez pas car il n'y a pas de mot de passe.
Pour définir un mot de passe, on utilise les droits admins et passwd:

```bash
sudo passwd abraracourcix
```
> Je vous laisse choisir le mot de passe, en cas d'oublie, refaites la commande précédente.

> Si vous avez le message "BAD PASSWORD: The password is shorter than 8 characters", vous pouvez continuer a retaper le mot de passe.

Nous allons faire aussi **panoramix**

```bash
sudo adduser panoramix
```

Je vous laisse définir un mot de passe pour panoramix.

Panoramix est un druide, il a donc son groupe.

```bash
sudo groupadd druide
```

Pour ajouter panoramix dans son groupe:

```bash
sudo usermod -a -G druide panoramix
```

Maintenant que le village est complet, il faut trois emplacements pour nos personnages:
 - le camp (pour cesar)
 - la forêt (pour panoramix)
 - le village (pour les gaulois)

Nous allons faire trois dossiers dans le dossier /gaule:

```bash
sudo mkdir -p /gaule/foret /gaule/village /gaule/camp
```

Puis pour affecter les droits:

```bash
sudo chown cesar /gaule/camp
```

> La commande chown change le propriétaire du fichier/dossier !

On le fait avec un groupe:

```bash
sudo chgrp gaulois /gaule/village
```

```bash
sudo chgrp druide /gaule/foret
```

> Attention, si les gaulois veulent écrire des fichiers dans leur espace, il faut donner les droits d'écritures !

Si vous faites **ls -l /gaule**, vous voyez que les propriétaires et groupes ont changé.

### Challenge me !

Mettons en pratique les commandes vues précédemment:

Q4: Je veux un utilisateur idefix

<details>
    <summary>Solution Q4</summary>
    
    sudo adduser idefix

</details>

Q5: Je veux qu'idefix puisse aller dans la forêt

<details>
    <summary>Solution Q5</summary>
    
    sudo chown idefix /gaule/foret

</details>

Q6: Je veux interdire l'accès à tout le monde à mon camp romain sauf à César

<details>
    <summary>Solution Q6</summary>
    
    sudo chmod go-rwx /gaule/camp

</details>

Vous venez de terminer le premier TP, si vous voulez un avant gout de la [session](https://www.cyberciti.biz/faq/show-all-running-processes-in-linux/) de [demain](https://librecours.net/module/sr/linux-ordinateur/logs.xhtml).