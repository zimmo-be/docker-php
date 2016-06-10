FROM centos:5

RUN yum install -y httpd php53 php53-cli php53-common php53-bcmath php53-gd \
            php53-imap php53-mbstring php53-mysql php53-pdo php53-snmp
RUN yum clean all

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composerv

RUN mkdir -p /var/www/project && \
    chown -R apache:apache /var/www/project && \
    ln -sf /dev/stdout /var/log/httpd/access_log && \
    ln -sf /dev/stderr /var/log/httpd/error_log

COPY php.ini /etc/php.d/project.ini
COPY vhost.conf /etc/httpd/conf.d/project.conf

WORKDIR /var/www/project

EXPOSE 80

ENTRYPOINT /usr/sbin/httpd -D FOREGROUND