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
- Ara es te que activar els mòduls d'apache2 necessaris:
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

- El primer pas per poder configurar el **MYSQL** es accedir a ell.
```bash
sudo mysql
```
- Una vegada dins de **MYSQL** crearem la base de dades a la que li posarem el nom de bbdd.
```bash
CREATE DATABASE bbdd;
```
- Amb la base de dades creada tenim que crear un usuario.
```bash
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
- Amb l'usuari creat li donem privilegis
```bash
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
```
- Ya hem fet tot al **MYSQL** a si que sortim
```bash
exit
```
- Una vegada ya fora del **MYSQL** el que farem sera probar la conexio a la base de dades
```bash
mysql -u usuario -p
```

## Descarreguem els fitxers de l'aplicació web
- Aquest es el arxiu que heu de descarregar
https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip
- Anem al directori baixadas
```bash
cd Baixades
```
- Una vegada dins del directori descomprimim allà els fitxers de l'aplicació web, heu de substituir `app-web.zip` per el nom del vostre fitxer que heu descarregat
```bash
sudo cp ~/Baixades/app-web.zip /var/www/html
```
- Anem al directori `/var/www/html`
```bash
cd /var/www/html
```
- Copiem els fitxers a la carpeta `/var/www/html`, modifiqueu `app-web` pel nom del directori on s'ha descomprimit el vostre arxiu.
```bash
sudo cp -R app-web/. /var/www/html
```

- Descomprim el arxiu heu de substituir `app-web.zip` per el nom del vostre fitxer
```bash
sudo unzip app-web.zip
```
- Una vegada hem descomprimit el `.zip` utilitzem aquest comandament per eliminar-lo. Recordem que el nom de `app-web`hi ha que cambiar-lo perl nom del teu arxiu.
```bash
sudo rm app-web.zip
```
- Una vegada eliminat el `.zip` tambe eliminem el `index.html`.
```bash
sudo rm -rf /var/www/html/index.html
```
## Aplicació de poders a les nostres aplicacions webs
- Una vegada hem descomprimit tots els arxius al directori `/var/www/html` li apliquem permisos a aquest directori.
- Si no estem dins del directori ya.
```bash
cd /var/www/html
```
- Una vegada dins del directori executarem aquests comandaments.
```bash
sudo chmod -R 775 .
```
```bash
sudo chown -R usuario:www-data .
```
