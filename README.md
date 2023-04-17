## How to Create MySQL with phpMyAdmin Docker Container
you will learn to launch MySQL Docker containers along with phpMyAdmin docker container using docker-compose command.

Docker-compose is an useful utility for managing multi-container docker applications. In our previous tutorial, I had discussed about the keep persistent data of MySQL docker containers using Docker volumes. Once you launched a MySQL container can be connect via terminal directly. But the phpMyAdmin lovers may need the web interface for managing databases.

So first create a docker-compose.yml file on your system with the following content.
docker-compose.yml:
```
version: '3'
 
services:
  db:
    image: mysql:5.7
    container_name: db
    environment:
      MYSQL_ROOT_PASSWORD: my_secret_password
      MYSQL_DATABASE: app_db
      MYSQL_USER: db_user
      MYSQL_PASSWORD: db_user_pass
    ports:
      - "6033:3306"
    volumes:
      - dbdata:/var/lib/mysql
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: pma
    links:
      - db
    environment:
      PMA_HOST: db
      PMA_PORT: 3306
      PMA_ARBITRARY: 1
    restart: always
    ports:
      - 8081:80
volumes:
  dbdata:
```
Next, run the following command to create Docker containers using the docker-compose.yml configuration file.
```
docker-compose up -d
```
