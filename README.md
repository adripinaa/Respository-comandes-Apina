# Instal·lació d'OwnCloud

## Instal·lació de la versió 7.4 de PHP a Ubnutu 24.04

Per a instal·lar l'OwnCloud cal tenir la versió 7.4 de PHP.

Les comandes següents són les necessàries per l'actualització de PHP.

Amb aquesta comanda instal·lem els requisits de PPA (arxius de paquets personals).

```bash

sudo apt install software-properties-common -y

```

Instal·lem les eines necessàries per poder treballar amb PPA.

```bash

LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y

```

Actualitzem

``` bash

sudo apt update

```

Amb aquestes 3 comandes instal·lem les llibreries de PHP de la versió 7.4.

``` bash

sudo apt install php7.4 -y

```

``` bash

sudo apt install -y php libapache2-mod-php7.4

```

``` bash

sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl

```

Amb aquesta comanda seleccionem la versió de PHP que necessitem, necessitem la 7.4.

``` bash

sudo update-alternatives --config phpmmm

```

Activem els mòduls que necessitem d'Apache2 perquè funcioni.

``` bash

sudo a2enmod proxy_fcgi setenvif

```

``` bash

sudo a2enconf php7.4-fpm

```

Finalment amb l'instal·lació de la versió 7.4 de PHP, reiniciem l'Apache2.

``` bash

sudo service apache2 restart

```

## Comandes per l'instal·lació i configuració de OwnCloud

Per a instal·lar i configurar OwnCloud, farem ús d'apache2, al instal·lar Apache2 es crearà una carpeta dins de /var/www/html, on treballarem.

## Comandes per l'instal·lació d'Apache2 i mysql, i llibreries de PHP

Actualitzem la nostra màquina.

``` bash

sudo apt update

```

Aquesta no és obligatòria posar-la, però és recomenable, triga molt en processar aquesta comanda.

``` bash

sudo apt upgrade

```

Instal·lem el servidor web d'Apache2

``` bash

sudo apt install -y apache2

```

Instal·lem la base de dades de mysql

``` bash

sudo apt install -y apache2

```

Instal·lem algunes llibreries PHP, que aquest és el llenguatge de totes les aplicacions.

``` bash

sudo apt install -y php libapache2-mod-php

```

``` bash

sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl

```

Finalment reiniciem el servidor d'Apache2

``` bash

sudo systemctl restart apache2

```

## Configurem la base de dades de mysql

### Entrem a la consola de dades de mysql per posar totes aquestes comandes.

Des d'un terminal on siguem root posem aquesta comanda per entrar a la terminal de mysql

``` bash

sudo mysql

```
![Captura desde 2024-11-07 14-06-07(1)](https://github.com/user-attachments/assets/a0477b29-fd8f-4859-8ee9-8aabf9b613f3)

### Creem una base de dades.

Dins el terminal de mysql creem una base de dades, al crear una nova s'ha creat aquesta nova base de dades, li posem bbdd

``` bash

CREATE DATABASE bbdd;

```
![Captura desde 2024-11-07 14-06-20](https://github.com/user-attachments/assets/ab8def8a-e326-4a43-b230-16809fb4167f)

### Creació del nostre usuari

Ara hem de crear un nou usuari, amb un usuari i una contrasenya, a més que utilitzarem la IP de localhost

``` bash

CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

```
![Captura desde 2024-11-07 14-06-57](https://github.com/user-attachments/assets/d1611068-eeaf-4d1d-b109-e6531834f477)

### Finalment li donem privilegis al nostre usuari

``` bash

GRANT ALL ON bbdd.* to 'usuario'@'localhost';

```
![Captura desde 2024-11-07 14-07-08](https://github.com/user-attachments/assets/e0b44991-d29e-46e2-a0d7-18a94b98d391)

### Sortim de la base de dades

``` bash

exit

```

### Ens assegurem que està tot bé.

Amb el terminal normal provem a connectar-nos a mysql i introduïm la nostra contrasenya de mysql.

``` bash

mysql -u usuario -p

```

## Descarreguem l'aplicació web

Descarreguem el .zip de la nostra cloud, la de OwnCloud:

https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip

Copiem el .zip i ho peguem al directori /var/www/html per fer tot el que ens falta. 

``` bash

sudo cp ~/Baixades/owncloud-complete-20240724.zip /var/www/html

```

Anem al directori /var/www/html

``` bash

cd /var/www/html

```

En aquest directori descomprimim el .zip que hem baixat.

``` bash

sudo unzip owncloud-complete-20240724.zip

```

Copiem els fitxers a la carpeta /var/www/html, i canviem els signes d'interrogant (??) pel nom del directori on s'ha descomprimit l'arxiu d'abans.

``` bash

sudo cp -R ??/. /var/www/html

```

La carpeta creada de quan hem descomprimit l'arxiu, l'esborrem (es torna a canviar per el nom de la carpeta).

``` bash

sudo rm -rf ??/

```

Eliminem el fitxer index.html de l'Apache2

``` bash

sudo rm -rf /var/www/html/index.html

```

## Permisos a les nostres aplicacions web.

Al tenir descomprimit el fitxer a /var/www/html donem permisos a aquest mateix directori amb les següents comandes.

``` bash

cd /var/www/html

```

``` bash

sudo chmod -R 775 .

```

``` bash

sudo chown -R usuario:www-data .

```

## Veure si podem accedir al navegador.

Entrem a http://localhost en el teu navegador web, i configura la teva Cloud.

Si hem fet bé tots els passos, ens ficarà a l'OwnCloud, i us demanarà crear-vos un usuari d'admin i la base de dades que has configurat.

La teva informació seria:

- Usuari: usuario

- Contrasenya: password

- Base de dades: bbdd

- Domini: localhost

I amb això ja hauries d'haver acabat de configurar i instal·lar la teva base de dades, i ja podries usar perfectament la teva Cloud.


# Configuracio d'ownCLoud
<p>Si has fet tot els pasos  bé t'hauria d'apareixer aixó:
  
![Captura desde 2024-11-12 08-36-23](https://github.com/user-attachments/assets/c679aa8f-b595-490b-bd02-a94b38cbba67)

## Creació d'usuaris
<p>Per crear usuaris anem on surt el nostre usuari.

![Captura desde 2024-11-12 08-38-12](https://github.com/user-attachments/assets/4942a1f6-0be6-4644-be9b-dc00ff0595c7)
<p>Fem clic a "users".
  
![Captura desde 2024-11-12 08-39-36](https://github.com/user-attachments/assets/1d38c658-3cd8-4e1c-ba9a-7e43ce801ea5)
<p>Aqui es on es crea l'usuari.
<p>Per crear l'usuari hem de posar el nostre nom d'usuari i un correu.
<p>Aquest pas es fa on posa el nostre usuari.
  
![Captura desde 2024-11-12 08-43-09](https://github.com/user-attachments/assets/a0487e98-c3f0-4e42-9fd3-b44ef4b53575)
<p>Ara creem 3 o 4 usuaris més.
  
![Captura desde 2024-11-12 08-52-23](https://github.com/user-attachments/assets/6b3332ea-27cc-47d8-9444-bf80ffd0b6bd)
## Assignem rols i permisos
<p> Ara assignarem rols al nostres usuaris creats.
<p> Per crear un rol hem de fer clic a "Add group", i ja tens dos rols creats que són: "Everyone" i "Admin".
  
![Captura desde 2024-11-12 08-57-00](https://github.com/user-attachments/assets/e74ad03a-7c27-4017-8729-3c131b37c6e5)
<p>Creem dos rols nous.
<p>Per assignar els rols en un usuari li donem a "Group" en el mateix usuari i l'assignem el rol que acabem de crear.
  
![Captura desde 2024-11-12 09-04-21](https://github.com/user-attachments/assets/a5ade8fe-e0fc-4842-a09b-3f475ed73654)
<p>Assignem permisos al nostres usuaris.
<p>Fem clic a "users" i a "Archivos"
<p>Seleccionem la carpeta a que volem donar permisos als nostres usuaris.
<p> Cliquem "sharing", posem el nom dels rols, o el nom de l'usuari.
  
![Captura desde 2024-11-12 09-23-02](https://github.com/user-attachments/assets/a0cecf31-4afb-426e-a607-99d41497a1ae)
![Captura desde 2024-11-12 09-25-46](https://github.com/user-attachments/assets/eae7ab17-c2b4-4360-9972-63722246f288)
<p>Amb aixo hauria d'haver finalitzat de configurar rols i permisos.
# Administració d'arxius.
<p>Per crear arxius, carpetes o pujar fitxers, Cliquem +.
  
![Captura desde 2024-11-12 09-40-19](https://github.com/user-attachments/assets/bc3ea617-71bd-49c2-9858-7d747505c964)
<p> Creem una carpeta.
<p> Ara creem un arxiu.
  
![Captura desde 2024-11-12 09-42-49](https://github.com/user-attachments/assets/6c899237-e4d3-4e4a-b84e-e9728ff47396)
<p> Aquest arxiu serveix com un document.

