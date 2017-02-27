FROM ubuntu:xenial

RUN apt-get update && \
    apt-get install -y software-properties-common python-software-properties && \
    locale-gen en_US.UTF-8 && export LANG=en_US.UTF-8 && \
    apt-get install -y curl git apache2 && \
    apt-get autoremove --purge php5-* && \
    add-apt-repository -y ppa:ondrej/php && apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y php7.1 php7.1-cli php7.1-common php7.1-bcmath php7.1-gd php7.1-imap php7.1-intl php7.1-mbstring \
    php7.1-mcrypt php7.1-mysql php7.1-soap php7.1-tidy php7.1-xml php7.1-gmp php-redis php-mongodb php7.1-sqlite3 php7.1-curl php7.1-zip && \
    apt-get clean

RUN a2enmod rewrite

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir -p /var/www/project && \
    chown -R www-data:www-data /var/www/project && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log

COPY php.ini /etc/php/7.1/apache2/conf.d/project.ini
COPY php.ini /etc/php/7.1/cli/conf.d/project.ini
COPY vhost.conf /etc/apache2/sites-available/000-default.conf

WORKDIR /var/www/project

EXPOSE 80

COPY httpd-foreground /usr/local/bin/

CMD ["httpd-foreground"]
