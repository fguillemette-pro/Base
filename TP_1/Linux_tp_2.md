# TP 02 - Linux
## Where is my host ?
Pour ce TP, il sera beaucoup moins guidé 😉:

### Step 1 - 
Installer un serveur web
```
sudo dnf install httpd
```
Vérifier son bon fonctionnement en allant sur l'adresse IP de votre machine

[Félicitation, vous êtes sur internet !](https://www.youtube.com/watch?v=ouEudC6rS8E)

### Step 2
Modifier le fichier index.html pour mettre votre nom/prénom/pseudo

### Step 3
Créer 2 users (korben,dallas)

### Step 4
Dans le fichier **/etc/httpd/conf.d/userdir.conf**:
- Commenter la ligne : UserDir disabled 
- Décommenter la ligne : UserDir public_html 
- Changer les lignes : 
```
  <Directory "/home/*/public_html">
    AllowOverride All     # change if you need
    Options None          # change if you need
    Require method GET POST OPTIONS
  </Directory>
```
- Redémarrer le service :
```
sudo systemctl restart httpd
```
- Créer un dossier public_html dans le home de korben et dallas **avec le compte !**
- Donner les droits 711 au home de korben et dallas
- Donner les droits 755 aux dossiers public_html
- Faites un fichier index.html avec un hello world dans public_html

Félicitation, vous êtes hebergeur web !

### Step 5

Depuis le log d'apache (votre serveur http), récupérer les accèes consernant korben dans un fichier nommé /home/korben/korben_web.log. (ce fichier doit être accessible à korben)

### Step 6

- Faites un fichier get_log_korben.sh dans le home de korben
- Copier " #!/bin/bash " en première ligne, puis la commande de l'étape 5
- Saisissez :
```
chmod +x get_log_korben.sh
```
- Pour executer votre script, saisissez:
```
./get_log_korben.sh
```
Félicitation, vous avez fait votre premier script !

### Step 7

On va automatiser la génération du fichier.
```
crontab -e
```
Puis à la fin du fichier:
```
* * * * * /home/korben/get_log_korben.sh >/dev/null 2>&1
```

### Step 8
Refaire **en script** les étapes 5,6 et 7 pour dallas

### Step 9
Complété le script fait à l'épate 8 avec la création de l'utilisateur lilou