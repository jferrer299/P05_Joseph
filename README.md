# P05_Joseph
Para desplegar aplicacviones web con Docker primero debemos crear las carpetas de ncada aplicacion (Adminer, Apache, Mediawiki, Guestbook y Wordpress)
Luego en cada carpeta debemps incluir un fichero de texto llamado docker-compose.yml 
Ahora especificaremos como lanzar cada aplicación:

ADMINER

https://hub.docker.com/_/adminer

version: '3.1'

services:

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

  db:
    image: mysql:5.6
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
      
      Esto es lo que debemos escribir en el fichero YAML/YML
      Abrimos docker 
      A continuación abrimos Visual Studio abrimos una terminal y nos ubicamos en la carpeta adminer y metemos el siguiente comando
      docker-compose up -d
      Con esto ya hemos desplegado la aplicacion y loo podremos ver en localhost.
      
      
      GUESTBOOK
      
      https://iesgn.github.io/curso_docker_2021/sesion5/guestbook.html
      
      version: '3.1'
services:
  app:
    container_name: guestbook
    image: iesgn/guestbook
    restart: always
    ports:
      - 80:5000
  db:
    container_name: redis
    image: redis
    restart: always
    
    
    
     Esto es lo que debemos escribir en el fichero YAML/YML
      nos ubicamos en la carpeta guestbook y metemos el siguiente comando
      docker-compose up -d
      Con esto ya hemos desplegado la aplicacion y loo podremos ver en localhost:**** y el puerto que hemos puesto.
      
      
      
      MEDIAWIKI
      
      https://hub.docker.com/_/mediawiki
      
      version: '3'
services:
  mediawiki:
    image: mediawiki
    restart: always
    ports:
      - 8080:80
    links:
      - database
    volumes:
      - images:/var/www/html/images
      # After initial setup, download LocalSettings.php to the same directory as
      # this yaml and uncomment the following line and use compose to restart
      # the mediawiki service
      # - ./LocalSettings.php:/var/www/html/LocalSettings.php
  database:
    image: mariadb
    restart: always
    environment:
      # @see https://phabricator.wikimedia.org/source/mediawiki/browse/master/includes/DefaultSettings.php
      MYSQL_DATABASE: my_wiki
      MYSQL_USER: wikiuser
      MYSQL_PASSWORD: example
      MYSQL_RANDOM_ROOT_PASSWORD: 'yes'
    volumes:
      - db:/var/lib/mysql

volumes:
  images:
  db:
  
  
    Esto es lo que debemos escribir en el fichero YAML/YML
      nos ubicamos en la carpeta mediawiki y metemos el siguiente comando
      docker-compose up -d
      Con esto ya hemos desplegado la aplicación y loo podremos ver en localhost:**** y el puerto que hemos puesto.
  
  
  WORDPRESS
  
  Fuente: https://aulasoftwarelibre.github.io/taller-de-docker/docker-compose/
  
  version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
      
      
      Esto es lo que debemos escribir en el fichero YAML/YML
      Nos ubicamos en la carpeta wordpress y metemos el siguiente comando
      docker-compose up -d
      Con esto ya hemos desplegado la aplicación y loo podremos ver en localhost.
      
      
      APACHE
      
      Fuente: https://www.foc.es/2021/10/06/6219-borrador-automatico-4.html
      
      version: '3.9'
services:
  apache:
    image: httpd:latest
    container_name: my-apache-app
    ports:
    - '8080:80'
    volumes:
    - ./website:/usr/local/apache2/htdocs
    
    
      Esto es lo que debemos escribir en el fichero YAML/YML
      Nos ubicamos en la carpeta apache y metemos el siguiente comando
      docker-compose up -d
      Con esto ya hemos desplegado la aplicación y loo podremos ver en localhost.
