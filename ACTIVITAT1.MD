# Moodle

Primer que tot el que necessites és una màquina virtual amb Ubuntu server 22.04.1 LTS, amb un adaptador pont a la interfície de xarxa.

![Moodle ](https://user-images.githubusercontent.com/114162326/206173667-4177f795-a197-43b5-bc8b-8b7a2e05b02e.png)
![Moodle AP](https://user-images.githubusercontent.com/114162326/206173683-1abf05ea-677e-4696-8b0e-ad067003cb16.png)

### SSH

Per a poder posar les comandes d'una manera més còmoda, el que he fet ha sigut connectar-me per SSH a la màquina virtual amb l'Ubuntu server.

```
ssh (nom_de_usuari)@(Ip_de_la_maquina)
```
![ssh 1](https://user-images.githubusercontent.com/114162326/206188967-fe294b30-9aaa-48d5-817b-ca216dcab6ec.png)

Tot seguit em demanara la contraseña.
![ssh 2](https://user-images.githubusercontent.com/114162326/206189565-8a8a1ba9-233b-4751-ac94-adee0f833205.png)

### Actualització dels paquets d'Ubuntu.

Primer que tot el que he fet a sigut actualitzar el paquets d'Ubuntu, per a no tenir cap problema a l'hora de instal·lar tot el que necessitem per al Moodle.

```
sudo apt-get update
```
![Install Apache 1](https://user-images.githubusercontent.com/114162326/206176671-352e0ae1-800c-4780-9942-cbac741730f9.png)

### Instal·lació Apache 2

Després d'actualitzar els paquets he instal·lat el servidor Apache 2 amb la següent comanda.

```
sudo apt-get install apache2
```
![Install apache 2](https://user-images.githubusercontent.com/114162326/206177895-39b2bdea-d2ca-41ff-a02b-0800cbc51b9d.png)

### Instal·lació de MariaDB

Una vegada instal·lat el servidor Apache 2, el que he fet ha sigut instal·lar la base de dades MariaDB, amb la següent comanda.

```
sudo apt-get install mariadb-server
```
![Instal Mariadb 1](https://user-images.githubusercontent.com/114162326/206178703-6ff0ffcb-bd39-4ec1-afbf-3fc72ff0a888.png)

Una vegada instal·lada la base de dades he executat la configuració de seguretat amb la següent comanda.

```
sudo mysql_secure_installation
```
![Install Mariadb 2](https://user-images.githubusercontent.com/114162326/206179117-80b01099-4cdc-4edb-9772-26ef55f71706.png)

### Instal·lació PHP7.3

Per a instal·lar PHP7.3 he utilitzat les següents comandes.

```
sudo apt-get install software-properties-common
```
![Install PHP 1](https://user-images.githubusercontent.com/114162326/206179818-155a796a-af83-400b-9e9a-4f353f36e2af.png)

```
sudo add-apt-repository ppa:ondrej/php
```
![Install PHP 2](https://user-images.githubusercontent.com/114162326/206180643-55258b40-4a46-4139-8f9f-86c25b7dc58a.png)

```
sudo apt-get update
```
![Install PHP 3](https://user-images.githubusercontent.com/114162326/206181151-8bdeeb80-84ba-40b1-bc67-9ff2475cf6a6.png)

```
sudo aptr-get install -y php7.3
```
![Install PHP4](https://user-images.githubusercontent.com/114162326/206181273-ac60b748-8dd9-48f1-8c57-ab83d4037e9d.png)

### Instal·lació Moodle

Primer que tot he instal·lat la versió 4.1 de Moodle amb la següent comanda.

```
wget https://download.moodle.org/download.php/direct/stable401/moodle-4.1.zip
```
![Install Moodle 1](https://user-images.githubusercontent.com/114162326/207822446-243ac6be-0999-4bc4-9cac-34f00518e8c3.png)

Tot seguit he descomprimit l'arxiu zip a la carpeta "/var/www/html/" amb la següent comanda.

```
sudo unzip moodle-4.1.zip.1 -d /var/www/html/
```
![Install Moodle 2](https://user-images.githubusercontent.com/114162326/207823556-881a1bb4-200c-4ed0-943a-4325d1781fb6.png)

Després de descomprimir l'arxiu el que he fet ha sigut canviar el propietari

```
sudo chown www-data:www-data /var/www/htlm/moodle/
```
![Install Moodle 3](https://user-images.githubusercontent.com/114162326/207824210-7669f3af-3ab7-4fa0-8b3f-6d5590a3b4ed.png)

He creat el directori per a guardar informacio dels usuaris al /home

```
sudo mkdir moodledata
ls
sudo chown www-data:www-data moodledata/
```

![Install Moodle 4](https://user-images.githubusercontent.com/114162326/207824739-7eaca3bc-4c37-4ee3-a50f-eeafb4b37afb.png)

### Configuració Base de Dades

El primer que he fet per configurar la Base de Dades del Moodle ha sigut obrir-la amb la comanda.

```
sudo mysql -u root -p
```
![Install Moodle 5](https://user-images.githubusercontent.com/114162326/207881580-9592b240-1764-4e1a-a43b-6151ed0271ad.png)

Tot seguit he creat l'usuari per a Moodle.

```
CREATE USER 'moodlemanager'@'localhost' IDENTIFIED Y 'managermoodle';
```
![Install Moodle 6](https://user-images.githubusercontent.com/114162326/207882041-8f1a94a5-a3e5-40f9-9a6f-51639a36013e.png)

Després he creat la Base de Dades per al Moodle.

```
CREATE DATABASE moodle;
```
![Install Moodle 7](https://user-images.githubusercontent.com/114162326/207882278-97ca7b1a-aaf5-4095-9f3d-648d78d84425.png)

Una vegada creada la Base de Dades, li he donat permís a l'usuari que he creat abans.

```
GRANT ALL PRIVILEGES ON moodle.* TO 'moodlemanager'@'localgost';
FLUSH PRIVILEGES;
```
![Install Moodle 8](https://user-images.githubusercontent.com/114162326/207882703-9c5da2d0-b07b-410b-9490-30214990a42f.png)

### Configuració del Moodle

Primer que tot hem demana que hi instali unes extensions de PHP.

```
sudo apt search php | grep curl
sudo apt install php73-curl
```
![Install extencio curl](https://user-images.githubusercontent.com/114162326/207902534-e4209891-96d6-4c74-87af-54c5a6411987.png)

```
sudo apt search php | greb zip
sudo apt install php7.3_zip
```
![Install extencion xmlrpc](https://user-images.githubusercontent.com/114162326/207902985-4e3402fa-b7fa-477f-9c15-ff91dd998305.png)

```
sudo apt-get isntall php7.3-xmlrpc
```
![Install extencion xmlrpc](https://user-images.githubusercontent.com/114162326/207903176-ec00cf74-7801-437f-834c-3b97c9474edc.png)

```
sudo apt-get install php7.3-mbstring
```
![Install extension mbstring](https://user-images.githubusercontent.com/114162326/207903331-822c7ba3-4b7d-434d-ad2a-5aa44f49331f.png)

Despres d'instal·lar les extencions he hagut d'accedir-hi pel navegador web de la màquina real.
![Configurar Moodle 1](https://user-images.githubusercontent.com/114162326/207889505-2ead5433-4e4c-4cb6-9f5c-203ee7fbc56f.png)

Tot seguit li he seleccionat l'idioma.
![Configurar Moodle 2](https://user-images.githubusercontent.com/114162326/207889674-8ab960d2-3d07-4120-a759-caf7b24fc566.png)

Una vegada posat l'idioma he posat la ruta a la Base de Dades que he creat anteriorment per al Moodle.
![Configurar moodle 3](https://user-images.githubusercontent.com/114162326/207890066-7502daf3-ec40-45e0-be8a-871fdc5399b5.png)

A continuació li he seleccionat la Base de Dades que hi havia instal·lat abans.
![Configurar Moodle 4](https://user-images.githubusercontent.com/114162326/207890429-1f7739cc-4b29-4527-b1fd-45246f2f316e.png)

Finalment, li he adjuntat la resta de la informació sobre la Base de Dades.
![Configurar Moodle 5](https://user-images.githubusercontent.com/114162326/207890881-0acbb2b2-e603-4f6a-8087-9431dadb7b02.png)

