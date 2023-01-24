# TP 02.1 - Linux
## Where is my host ?
Pour ce TP, il sera beaucoup moins guidé 😉:

### Fail2ban

On va faire un peu de securité, je vous propose un outil, fail2ban, bien pratique pour bloquer les bots qui tentent de se connecter à votre serveur.

Il nous faut des dépots supplémentaires:

```bash
dnf install epel-release
```

Puis on installe les paquets:

```bash
dnf install sl fail2ban fail2ban-firewalld
```

On démarre le service fail2ban:

```bash
systemctl start fail2ban
```

[Optionnel] Sous les systèmes de la famille Redhat, cette commande permet d'activer le démarrage du service au boot du système.

```bash
systemctl enable fail2ban
```

On controle le status du service:

```bash
systemctl status fail2ban
```

Pour éviter d'éditer le fichier de configuration principal, on fait une copie du fichier qui prendra notre configuration:

```bash
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

```bash
vim /etc/fail2ban/jail.local
```

En dessous de la section [DEFAULT], vous voyez trois valeurs:

* Le temps de bannissement (bantime)
* La période entre les essaies (findtime)
* Le nombre d'essaie (maxretry)

```
bantime = 1h
findtime = 1h
maxretry = 5
```

Nous allons ensuite configurer fail2ban pour qu'il utilise firewalld ([et non openoffice](https://www.youtube.com/watch?v=F011hLZHZrM))

```bash
mv /etc/fail2ban/jail.d/00-firewalld.conf /etc/fail2ban/jail.d/00-firewalld.local
```

Pour appliquer les changements:

```bash
systemctl restart fail2ban && sl
```

Si un train vient de passer, tu devrais faire attention à tes copiers/collers

Vérifier que votre service est bien redémarré (systemctl status).

Nous allons demander à fail2ban de surveiller le serveur ssh.

Nous allons faire un fichier:

```bash
vim /etc/fail2ban/jail.d/sshd.local
```

Avec le contenu suivant:

```
[sshd]
enabled = true

# Override the default global configuration
# for specific jail sshd
bantime = 1d
maxretry = 3
```

On redémarre notre service:

```bash
systemctl restart fail2ban
```

La jail devrait être visible:

```bash
fail2ban-client status
```

Pour confirmer que fail2ban à bien pris votre fichier de configuration:

```bash
fail2ban-client get sshd maxretry
```

Depuis **une autre vm**, connectez vous avec un mot de passe faux, puis vérifier la jail avec cette commande: 

```bash
fail2ban-client status sshd
```

Pour débannir une ip:

```bash
fail2ban-client unban [IP]
```

Félicitation, vous avez protégé votre serveur SSH des bots

