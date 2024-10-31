# OwnCloud
Instal·larem el núvol OwnCloud des de la terminal en un programari Linux.
## Primer paso Instal·lació d'apache2, mysql i algunes llibreries al contenidor
Abans de fer aixo el que farem sera actualitzar la maquina.
Amb l'us del comandament 
```bash
sudo apt update
```
- Una vegada executat aquest comandament farem aquest altre 

```bash
sudo apt upgrade
```

- Una vegada executat aqust 2 comandaments ya tenim la maquina actualizada i es el moment de instalar **apache2 i mysql**
- Per fer aixo utilitzarem aquests comandaments:
```bash
sudo apt install -y apache2**
```
```bash
sudo apt install -y mysql-server
```

- Ara ja tenim les aplicacions instalades, ara instalarem libreries de les diferents aplicaions: 
```bash
sudo apt install -y php libapache2-mod-php
```
```bash
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

- Una vegada instala les aplicaions i les librerires reinitciarem el servidor d'apache2
```bash
sudo systemctl restart apache2
```
## Instal·lar la versió 7.4 de PHP a Ubuntu 24.04

- Per a poder instal·lar ownCloud necessitarem la versió 7.4 de PHP, per a instal·lar-la al nostre sistema haurem de fer les següents comandes:
- Instal·leu els requisits previs de PPA:

```bash
sudo apt install software-properties-common -y
```
- Instal·la les eines necessàries per treballar amb els arxius de paquets personals (PPA).

```bash
LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
```
- Actualitza ara els repositoris:
```bash
sudo apt update
```
- Una vegada actulitzats els repositoris instalem les llibreries de PHP de la versió 7.4
```bash
sudo apt install php7.4 -y
```
```bash
sudo apt install -y php libapache2-mod-php7.4
```
```bash
sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl
```
- Una vegada instalades les llibreries seleccioneu la versió de PHP que voleu:
```bash
sudo update-alternatives --config php
```
Ara es te que activar els mòduls d'apache2 necessaris:
```bash
sudo a2enmod proxy_fcgi setenvif
```
```bash
sudo a2enconf php7.4-fpm
```
- I pre ultim tornem a actualitzar apache2
```bash
sudo service apache2 restart
```
## Configurem el MYSQL

El primer pas per poder configurar el **MYSQL** es accedir a ell.

**sudo mysql**

Una vegada dins de **MYSQL** crearem la base de dades a la que li posarem el nom de bbdd.

**CREATE DATABASE bbdd;**

Amb la base de dades creada tenim que crear un usuario.

CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

Amb l'usuari creat li donem privilegis

GRANT ALL ON bbdd.* to 'usuario'@'localhost';

Ya hem fet tot al **MYSQL** a si que sortim

**exit**

