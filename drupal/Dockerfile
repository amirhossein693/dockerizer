FROM php:8.1-fpm
LABEL maintainer="amirhossein693@gmail.com"
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN apt-get update && apt-get install -y \
	zip \
    	unzip \
    	nano \
    	libzip-dev \
	curl \
	git \
        libpq-dev \
        libicu-dev \
        zlib1g-dev \
        libpng-dev \
        libjpeg-dev \
        libfreetype6-dev \
        postgresql-client \
   && docker-php-ext-configure \
        gd --with-jpeg --with-freetype \    
   && docker-php-ext-install \
        gd \
        bcmath \
        opcache \
        pdo \
        pdo_pgsql \
	zip \
    && docker-php-ext-enable \
        gd \
        bcmath \
        opcache \
        pdo \
        pdo_pgsql

COPY php.ini /usr/local/etc/php
        
RUN curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
RUN HASH=`curl -sS https://composer.github.io/installer.sig`
RUN php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/html
COPY code .
RUN composer install
