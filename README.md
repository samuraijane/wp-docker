# wp-docker

Use this software to run Wordpress and MySQL using Docker containers.

### Prerequisites
Be sure that the needed docker images are on your machine
1. `docker pull mysql`
2. `docker pull phpmyadmin/phpmyadmin`
3. `docker pull wordpress`

### Instructions
1. `git clone https://github.com/samuraijane/wp-docker.git`
2. `cd wp-docker`
3. `docker-compose up -d`

### Browser Access
1. _phpMyAdmin_ runs at **localhost:8080**
2. _Wordpress_ runs at **localhost**

### Observations
Some threads have mentioned issues with the file upload size being too small. To increase the size, you will need to first create a file named "uploads.ini" in the root of the project. Then modify "docker-compose.yml" from this:

```
volumes: ["./wp-content:/var/www/html/wp-content"]
```

to this:

```
volumes: ["./wp-content:/var/www/html/wp-content", "./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini"]
```

The contents of "uploads.ini" should include the following:

```
file_uploads = On
memory_limit = 64M
upload_max_filesize = 64M
post_max_size = 64M
max_execution_time = 600
```

SOURCES
1. [Docker Forum](https://forums.docker.com/t/how-to-get-access-to-php-ini-file/68986)
2. [Github Thread](https://github.com/docker-library/wordpress/issues/375)
