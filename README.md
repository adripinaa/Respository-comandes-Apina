# Respository-comandes-Apina
Instal·lació i configuració de aplicacions web, Instal·lació d'apache2, mysql i algunes llibreries al contenidor
1. Actualització: sudo apt update, sudo apt upgrade

2. Instal·lació del servidor web apache2: sudo apt install -y apache2

3. Instal·lació del servidor de bases de dades mysql-server: sudo apt install -y mysql-server

4. Instal·lació d'algunes llibreries de php, el llenguatge principal que utilitzen les aplicacions.

5. Instal·lació d'algunes llibreries de php, el llenguatge principal que utilitzen les aplicacions: sudo apt install -y php libapache2-mod-php, sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl

6. Reiniciar el servidor de l'apache 2: sudo systemctl restart apache2

Configuració de MySQL
Accedim a la consola de MySQL

1. Obrim el terminal on siguem root hem d'executar la següent comanda: sudo mysql

Creació de la base de dades:
1. Un cop dins la consola de MySQL executem les comandes per crear la base de dades. Estem creant una base de dades amb el nom bbdd: CREATE DATABASE bbdd;

2. Creació d'un usuari: Has de tenir en compte que s'haurà d'identificar la IP des de la qual s'accedirà a la base de dades, en aquest cas, localhost: CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

3. Privliegis per l'usuari: GRANT ALL ON bbdd.* to 'usuario'@'localhost';

4. Sortir de la base de dades: exit

5. Probar la connexió de la base de dades: mysql -u usuario -p

6. Canviem l'accés per defecte a la nostra màquina: vim /etc/mysql/mysql.conf.d/mysqld.cnf

7. Busquem la línia següent: bind-address = 127.0.0.1

8. Hem de canviar el bind-address per 0.0.0.0 i la línia ha de quedar així: bind-address = 0.0.0.0

9. Reiniciem el servidor: systemctl restart mysql

10. Creació d'un usuari per a accedir des d'una màquina remota: CREATE USER 'usuario'@'192.168.22.100' IDENTIFIED WITH mysql_native_password BY 'password';

11. Hem de donar privilegis a l'usuari que accedirà des de la màquina remota. Per accedir des de fora, hauriem de donar-li també privilegis a l'usuari a l'altra màquina: GRANT ALL ON bbdd.* to 'usuario'@'192.168.22.100';, exit

    Descarreguem els fitxers de l'aplicació web

    1. Anem al directori /var/www/html i descomprimim allà els fitxers de l'aplicació web, heu de substituir app-web.zip per el nom del vostre fitxer que heu descarregat amb l'aplicació web i el nom de la carpeta app-web per la carpeta que us ha creat, si la vostra instal·lació de linux està en un idioma diferent al català, no tindreu la carpeta Baixades, modifiqueu la comanda per adaptarla a les vostrs necessitats:
   
    2. sudo cp ~/Baixades/app-web.zip /var/www/html

    3. Aneu al directori: /var/www/htmlcd /var/www/html

    4. Descomprimiu el fitxer que heu baixat: sudo unzip app-web.zip

    5. Copieu els fitxers a la carpeta: /var/www/html, modifiqueu app-web pel nom del directori on s'ha descomprimit el vostre arxiu; sudo cp -R app-web/. /var/www/html

    6. Eliminem la carpeta creada quan hem fet l'unzip: sudo rm -rf app-web/
   
       Eliminem el fitxer index.html de l'apache2: sudo rm -rf /var/www/html/index.html

Aplicació de permisos a les nostres aplicacions web

Un cop descomprimits els fitxers de l'aplicació web al directori /var/www/html, apliquem els següents permisos al directori:

/var/www/html, cd /var/www/html

sudo chmod -R 775 .

sudo chown -R usuario:www-data .

Accedim al navegador per veure que tot funciona, poseu la direcció: http://localhost al navegador web i configureu la cloud.

Si tot ha anat bé i heu seguit el manual us apareixerà l'instal·lador de l'aplicació web que heu baixat i us demanarà crear un usuario admin i la informació de la base de dades.

La informació que heu de posar (si no heu modificat la informació del manual) és la següent:

    usuari: usuario
    contrasenya: password
    base de dades: bbdd
    domini: localhost









