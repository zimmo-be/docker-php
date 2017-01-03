# Supported tags and respective Dockerfile links

#### Apache

* 7.1-apache-ubuntu [(7.1/apache/ubuntu/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/7.1/apache/ubuntu/Dockerfile)
* 7.0-apache-oraclelinux [(7.0/apache/oraclelinux/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/7.0/apache/oraclelinux/Dockerfile)
* 5.6-apache-oraclelinux [(5.6/apache/oraclelinux/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/5.6/apache/oraclelinux/Dockerfile)
* 5.5-apache-oraclelinux [(5.5/apache/oraclelinux/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/5.5/apache/oraclelinux/Dockerfile)
* 5.3-apache-centos-5 [(5.3/apache/centos-5/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/5.3/apache/centos-5/Dockerfile)

#### FPM

* 7.0-fpm-oraclelinux [(7.0/fpm/oraclelinux/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/7.0/fpm/oraclelinux/Dockerfile)
* 7.0-fpm-alpine [(7.0/fpm/alpine/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/7.0/fpm/alpine/Dockerfile)
* 7.1-fpm-alpine [(7.1/fpm/alpine/Dockerfile)](https://github.com/zimmo-be/docker-php/blob/master/7.1/fpm/alpine/Dockerfile)

# How to use this image

#### Apache

    php:
      image: zimmobe/php:7.0-apache-oraclelinux
      volumes:
        - .:/var/www/project/
      environment:
        - SYMFONY_ENV=dev
        - SYMFONY_DEBUG=1
      links:
        - mongodb
      ports:
        - 80
    
    mongodb:
      image: mongo:3.2

#### FPM

    php:
      image: zimmobe/php:7.0-fpm-alpine
      volumes:
        - .:/var/www/project/
      environment:
        - SYMFONY_ENV=dev
        - SYMFONY_DEBUG=1
      links:
        - mongodb
    
    nginx:
      image: nginx:1.10-alpine
      volumes:
          - .:/var/www/project/
      links:
        - php
      ports:
        - 80
    
    mongodb:
      image: mongo:3.2
