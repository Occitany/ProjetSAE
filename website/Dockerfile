# Utilise l'image de base php:apache pour Symfony
FROM php:8.1-apache

# Installe les dépendances nécessaires et lie le fichier de configuration du web server.
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf \
  \
  && apt-get update \
  && apt-get install -qq -y --no-install-recommends \
     cron \
     vim \
     locales coreutils apt-utils git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev \
  \
  &&  echo "en_US.UTF-8 UTF-8" > /etc/locale.gen  \
  &&  echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
  &&  locale-gen \
  \
  &&  curl -sS https://getcomposer.org/installer | php -- \
  &&  mv composer.phar /usr/local/bin/composer 
  
RUN docker-php-ext-configure intl 

RUN docker-php-ext-install pdo pdo_mysql mysqli gd opcache intl zip calendar dom mbstring zip gd xsl && a2enmod rewrite 
RUN pecl install apcu && docker-php-ext-enable apcu
    
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions amqp

WORKDIR /var/www

