FROM oraclelinux:7

RUN yum install -y yum-plugin-ovl \
    && rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm \
    && yum update -y \
    && yum reinstall -y glibc-common \
    && yum install -y \
        git httpd \
        php55w php55w-cli php55w-common php55w-bcmath php55w-gd php55w-imap php55w-intl php55w-mbstring \
        php55w-mcrypt php55w-mysql php55w-pdo php55w-pear php55w-soap php55w-tidy php55w-xml \
    && yum clean all

RUN yum install -y php55w-devel gcc openssl-devel make \
    && pecl install mongodb \
    && echo "extension=mongodb.so" > /etc/php.d/mongodb.ini \
    && yum remove -y php55w-devel gcc openssl-devel make \
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
