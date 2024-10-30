# OwnCloud
Instal·larem el núvol OwnCloud des de la terminal en un programari Linux.
## Primer paso Instal·lació d'apache2, mysql i algunes llibreries al contenidor
Abans de fer aixo el que farem sera actualitzar la maquina.
Amb l'us del comandament 

**sudo apt update**

Aixo es el que te que surtir al executar el comandament

Una vegada executat aquest comandament farem aquest altre 

**sudo apt upgrade**

Una vegada executat aqust 2 comandaments ya tenim la maquina actualizada i es el moment de instalar **apache2 i mysql**
Per fer aixo utilitzarem aquests comandaments:

- **sudo apt install -y apache2**
- **sudo apt install -y mysql-server**

Ara ja tenim les aplicacions instalades, ara instalarem libreries de les diferents aplicaions: 

- **sudo apt install -y php libapache2-mod-php**
- **sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl**

Una vegada instala les aplicaions i les librerires reinitciarem el servidor d'apache2

**sudo systemctl restart apache2**

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

