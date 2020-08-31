FROM amazonlinux:latest
# update and install some utilities
RUN yum update -y && \
    yum clean all && \
    yum install git tar gzip -y
# install Epel php7.4 and nginx 
RUN amazon-linux-extras install epel php7.4 httpd_modules nginx1 -y

RUN yum install -y supervisor php php-{mbstring,xml,gd,curl,gettext,intl,opcache,pecl-apcu,pecl-apcu-devel}
# inscrease limits on php.ini
ENV OSTICKET_VERSION 1.14.x

RUN sed -i 's/\(^memory_limit =\).*/memory_limit = 256M/g' /etc/php.ini && \
    sed -i 's/\(^upload_max_filesize =\).*/upload_max_filesize = 2G/g' /etc/php.ini && \
    sed -i 's/\(^post_max_size =\).*/post_max_size = 2G/g' /etc/php.ini && \
    sed -i 's/\(^max_execution_time =\).*/max_execution_time = 600/g' /etc/php.ini &&  \
    sed -i 's/\(^user = \).*/user = nginx/g' /etc/php-fpm.d/www.conf && \
    sed -i 's/\(^group = \).*/user = nginx/g' /etc/php-fpm.d/www.conf

RUN mkdir -p /usr/share/nginx/html/osticket
WORKDIR /opt

RUN git clone -b $OSTICKET_VERSION https://github.com/osTicket/osTicket

WORKDIR /opt/osTicket
RUN php manage.php deploy --setup /usr/share/nginx/html/osticket

RUN rm -rf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
COPY supervisord.conf /etc/supervisord.conf
#ENTRYPOINT [ "/usr/bin/supervisord" ]
CMD ["/usr/bin/supervisord"]

