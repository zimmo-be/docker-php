FROM centos:5

RUN yum install -y wget httpd php53 php53-cli php53-common php53-bcmath php53-gd \
            php53-imap php53-mbstring php53-mysql php53-pdo php53-snmp
RUN yum clean all

WORKDIR /home

RUN wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm
RUN rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt
RUN rpm -K rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm
RUN rpm -i rpmforge-release-0.5.2-2.el5.rf.x86_64.rpm
RUN yum install -y git

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composerv

RUN mkdir -p /var/www/project && \
    chown -R apache:apache /var/www/project && \
    ln -sf /dev/stdout /var/log/httpd/access_log && \
    ln -sf /dev/stderr /var/log/httpd/error_log

COPY php.ini /etc/php.d/project.ini
COPY vhost.conf /etc/httpd/conf.d/project.conf

WORKDIR /var/www/project

EXPOSE 80

COPY httpd-foreground /usr/local/bin/

CMD ["/usr/local/bin/httpd-foreground"]