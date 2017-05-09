FROM php:7.0-apache

# Run install mysql PDO and enable mode rewrite
RUN docker-php-ext-install pdo_mysql

# Copy apache conf and php.ini conf
COPY ./misc/apache2.conf /etc/apache2/apache2.conf
COPY ./misc/ports.conf /etc/apache2/ports.conf
COPY ./misc/php.ini /usr/local/etc/php/php.ini

COPY . /var/www/html

#  Configuring Apache
RUN sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=root/g' /etc/apache2/envvars &&\
    rm /etc/apache2/sites-available/000-default.conf &&\
    rm /etc/apache2/sites-enabled/000-default.conf &&\
    chgrp -R root /var/run/apache2* /var/lock/apache2* &&\
    chmod -R ug+rwx /var/run/apache2* /var/lock/apache2* &&\
    a2enmod rewrite 

WORKDIR /var/www/html

EXPOSE 8080 8443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]