# OwnCloud
Instal·larem el núvol OwnCloud des de la terminal en un programari Linux.
## Primer paso Instal·lació d'apache2, mysql i algunes llibreries al contenidor
Abans de fer aixo el que farem sera actualitzar la maquina.
Amb l'us del comandament 
```console
sudo apt update
```
1. Una vegada executat aquest comandament farem aquest altre 

```console
sudo apt upgrade
```
2. Una vegada executat aqust 2 comandaments ya tenim la maquina actualizada i es el moment de instalar **apache2 i mysql** utilitzarem aquests comandaments:
   
```console
sudo apt install -y apache2**
```
```console
sudo apt install -y mysql-server
```

4. Ara ja tenim les aplicacions instalades, ara instalarem libreries de les diferents aplicaions: 
```console
sudo apt install -y php libapache2-mod-php
```
```console
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```
5. Una vegada instala les aplicaions i les librerires reinitciarem el servidor d'apache2

```console
sudo systemctl restart apache2
```
## Instal·lar la versió 7.4 de PHP a Ubuntu 24.04

1. Per a poder instal·lar ownCloud necessitarem la versió 7.4 de PHP, per a instal·lar-la al nostre sistema haurem de fer les següents comandes:
2. Instal·leu els requisits previs de PPA:

```console
sudo apt install software-properties-common -y
```
3. Instal·la les eines necessàries per treballar amb els arxius de paquets personals (PPA).

```console
LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
```
4. Actualitza ara els repositoris:
```console
sudo apt update
```
5. Una vegada actulitzats els repositoris instalem les llibreries de PHP de la versió 7.4
```console
sudo apt install php7.4 -y
```
```console
sudo apt install -y php libapache2-mod-php7.4
```
```console
sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl
```
6. Una vegada instalades les llibreries seleccioneu la versió de PHP que voleu:
```console
sudo update-alternatives --config php
```
7. Ara es te que activar els mòduls d'apache2 necessaris:
```console
sudo a2enmod proxy_fcgi setenvif
```
```console
sudo a2enconf php7.4-fpm
```
8. I pre ultim tornem a actualitzar apache2
```console
sudo service apache2 restart
```
## Configurem el MYSQL

1. El primer pas per poder configurar el **MYSQL** es accedir a ell.
```console
sudo mysql
```
2. Una vegada dins de **MYSQL** crearem la base de dades a la que li posarem el nom de bbdd.
```console
CREATE DATABASE bbdd;
```
3. Amb la base de dades creada tenim que crear un usuario.
```console
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
4. Amb l'usuari creat li donem privilegis
```console
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
```
5. Ya hem fet tot al **MYSQL** a si que sortim
```console
exit
```
6. Una vegada ya fora del **MYSQL** el que farem sera probar la conexio a la base de dades
```console
mysql -u usuario -p
```

## Descarreguem els fitxers de l'aplicació web
1. Aquest es el arxiu que heu de descarregar
https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip
2. Anem al directori baixadas
```console
cd Baixades
```
3. Una vegada dins del directori descomprimim allà els fitxers de l'aplicació web, heu de substituir `app-web.zip` per el nom del vostre fitxer que heu descarregat
```console
sudo cp ~/Baixades/app-web.zip /var/www/html
```
4. Anem al directori `/var/www/html`
```console
cd /var/www/html
```
5. Copiem els fitxers a la carpeta `/var/www/html`, modifiqueu `app-web` pel nom del directori on s'ha descomprimit el vostre arxiu.
```console
sudo cp -R app-web/. /var/www/html
```

6. Descomprim el arxiu heu de substituir `app-web.zip` per el nom del vostre fitxer
```console
sudo unzip app-web.zip
```
7. Una vegada hem descomprimit el `.zip` utilitzem aquest comandament per eliminar-lo. Recordem que el nom de `app-web`hi ha que cambiar-lo perl nom del teu arxiu.
```console
sudo rm app-web.zip
```
8. Una vegada eliminat el `.zip` tambe eliminem el `index.html`.
```console
sudo rm -rf /var/www/html/index.html
```
## Aplicació de poders a les nostres aplicacions webs
1. Una vegada hem descomprimit tots els arxius al directori `/var/www/html` li apliquem permisos a aquest directori.
2. Si no estem dins del directori ya.
```console
cd /var/www/html
```
3. Una vegada dins del directori executarem aquests comandaments.
```console
sudo chmod -R 775 .
```
```console
sudo chown -R usuario:www-data .
```

 
