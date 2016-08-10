FROM oraclelinux:7

RUN yum install -y yum-plugin-ovl && \
    rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm && \
    yum update -y && \
    yum install -y \
        git httpd \
        php70w php70w-cli php70w-common php70w-bcmath php70w-gd php70w-imap php70w-intl php70w-mbstring \
        php70w-mcrypt php70w-mysql php70w-pdo php70w-pear php70w-soap php70w-tidy php70w-xml php70w-pecl-redis && \
    yum clean all

RUN yum install -y php70w-devel gcc openssl-devel make && \
    pecl install mongodb && \
    echo "extension=mongodb.so" > /etc/php.d/mongodb.ini && \
    yum remove -y php70w-devel gcc openssl-devel make && \
    yum autoremove -y && \
    yum clean all

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir -p /var/www/project && \
    chown -R apache:apache /var/www/project && \
    ln -sf /dev/stdout /var/log/httpd/access_log && \
    ln -sf /dev/stderr /var/log/httpd/error_log

COPY php.ini /etc/php.d/project.ini
COPY vhost.conf /etc/httpd/conf.d/project.conf

WORKDIR /var/www/project

EXPOSE 80

COPY httpd-foreground /usr/local/bin/

CMD ["httpd-foreground"]
