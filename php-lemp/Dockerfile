FROM debian:12


#Instalar paquetes necesarios (apache php extensions php)
RUN apt update && apt install -y php-fpm libapache2-mod-php \
    curl \
    wget \
    git \
    zip \
    php-json php-xml php-zip php-gd php-mysql  php-intl \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

#Activar módulos de apache

RUN a2enmod rewrite
RUN a2enmod ssl


#Instalar composer

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('composer-setup.php'); exit(1); }"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"

#Instalar ferramentas npm se son necesarias


EXPOSE 9000

#Instrución para arrancar apache
#CMD ["apache2ctl", "-D", "FOREGROUND"]
CMD ["php8.2-fpm", "-F"]