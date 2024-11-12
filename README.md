REPOSITORY COMANDES ADRIAM

Instal·lació i configuració d'aplicacions web, així com d'Apache2, MySQL i algunes biblioteques al contenidor.

Instal·lació d'Apache2, MySQL i PHP

1. Actualització del sistema: Executem la comanda per actualitzar: sudo apt update i, a continuació, sudo apt upgrade.


2. Instal·lació del servidor web Apache2: Amb la següent comanda instal·lem Apache2: sudo apt install -y apache2.


3. Instal·lació del sistema de gestió de bases de dades MySQL: Fem la instal·lació amb: sudo apt install -y mysql-server.


4. Instal·lació de llibreries per a PHP: PHP és el llenguatge principal utilitzat en aquestes aplicacions.


5. Instal·lació de llibreries PHP addicionals: Executem: sudo apt install -y php libapache2-mod-php i també sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl.


6. Reiniciar el servidor Apache2: Per aplicar els canvis, reiniciem Apache amb la comanda: sudo systemctl restart apache2.



Configuració de MySQL

1. Accés a la consola de MySQL: Obrim el terminal com a root i executem: sudo mysql.



Creació de la base de dades i usuari:

1. Creació de la base de dades: Un cop dins de MySQL, creem la base de dades amb la comanda: CREATE DATABASE bbdd;.


2. Creació d'un usuari MySQL: Configurem l'usuari especificant l'adreça IP local (localhost) des de la qual accedirà: CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';.


3. Assignació de permisos: Donem permisos totals a l'usuari sobre la base de dades amb: GRANT ALL ON bbdd.* TO 'usuario'@'localhost';.


4. Sortir de la consola de MySQL: Amb la comanda exit.


5. Verificació de la connexió: Comprovem la connexió amb la base de dades executant: mysql -u usuario -p.


6. Modificació de la configuració d'accés: Obrim el fitxer de configuració amb l'editor Vim: vim /etc/mysql/mysql.conf.d/mysqld.cnf.


7. Trobar la línia de bind-address: Cerquem la línia bind-address = 127.0.0.1.


8. Modificar el bind-address: Canviem la IP per 0.0.0.0 de manera que la línia quedi així: bind-address = 0.0.0.0.


9. Reiniciar el servidor MySQL: Aplicar els canvis amb la comanda: systemctl restart mysql.


10. Creació d'un usuari per a accés remot: Definim un usuari amb permís per accedir des d'una IP específica (192.168.22.100) amb: CREATE USER 'usuario'@'192.168.22.100' IDENTIFIED WITH mysql_native_password BY 'password';.


11. Permisos per a l'usuari remot: Donem permisos a l'usuari remot per accedir a la base de dades: GRANT ALL ON bbdd.* TO 'usuario'@'192.168.22.100'; i després, exit.



Descarregar els fitxers de l'aplicació web

1. Accedir al directori HTML: Descomprimim els fitxers de l'aplicació a /var/www/html. Hem de substituir app-web.zip pel nom del fitxer que hàgiu descarregat i app-web pel nom del directori creat.


2. Copiar el fitxer ZIP: Executem sudo cp ~/Baixades/app-web.zip /var/www/html.


3. Navegar al directori web: Amb la comanda: cd /var/www/html.


4. Descomprimir l'arxiu ZIP: Fem servir: sudo unzip app-web.zip.


5. Copiar els fitxers al directori web principal: Canviem app-web pel nom de la carpeta descomprimida: sudo cp -R app-web/. /var/www/html.


6. Eliminar la carpeta descomprimida: Eliminem el directori temporal creat amb: sudo rm -rf app-web/. També podem esborrar el fitxer d'index per defecte d'Apache amb: sudo rm -rf /var/www/html/index.html.



Aplicació de permisos

Un cop descomprimits els fitxers de l'aplicació web a /var/www/html, assignem els permisos:

1. Establir permisos: Accedim al directori amb cd /var/www/html.


2. Modificar els permisos: Executem sudo chmod -R 775 ..


3. Canviar propietari i grup: Fem que usuario sigui el propietari i www-data el grup amb: sudo chown -R usuario:www-data ..



Verificació de la instal·lació al navegador

Per comprovar que tot funciona, obrim el navegador i introduïm l'adreça: http://localhost. Si s'ha configurat correctament, apareixerà la pantalla d'instal·lació de l'aplicació web que hem descarregat.

Informació d'accés a la base de dades:

Usuari: usuario

Contrasenya: password

Base de dades: bbdd

Domini: localhost


Si has seguit aquest manual correctament, podràs completar la instal·lació de l'aplicació web.
