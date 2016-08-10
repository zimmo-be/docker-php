FROM oraclelinux:7

RUN yum install -y yum-plugin-ovl \
    && rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm \
    && yum update -y \
    && yum install -y \
        httpd \
        php56w php56w-cli php56w-common php56w-bcmath php56w-gd php56w-imap php56w-intl php56w-mbstring \
        php56w-mcrypt php56w-mysql php56w-opcache php56w-pdo php56w-pear php56w-soap php56w-tidy php56w-xml \
    && yum clean all

RUN yum install -y php56w-devel gcc openssl-devel make \
    && pecl install mongo \
    && echo "extension=mongo.so" > /etc/php.d/mongo.ini \
    && yum remove -y php56w-devel gcc openssl-devel make \
    && yum autoremove -y \
    && yum clean all

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir -p /var/www/project \
    && chown -R apache:apache /var/www/project \
    && ln -sf /dev/stdout /var/log/httpd/access_log \
    && ln -sf /dev/stderr /var/log/httpd/error_log

COPY php.ini /etc/php.d/project.ini
COPY vhost.conf /etc/httpd/conf.d/project.conf

WORKDIR /var/www/project

EXPOSE 80

COPY httpd-foreground /usr/local/bin/

CMD ["httpd-foreground"]
