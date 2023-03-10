ARG PHP_VERSION=8.1

FROM php:$PHP_VERSION-fpm-alpine


# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# Install php modules
RUN apk add libzip-dev libxml2-dev libpng-dev autoconf make binutils-gold g++ gcc imagemagick-dev imagemagick freetype-dev libjpeg-turbo-dev msttcorefonts-installer fontconfig && \
    update-ms-fonts

RUN docker-php-ext-configure gd --with-jpeg --with-freetype && \
    docker-php-ext-install zip soap gd mysqli pdo pdo_mysql opcache \
    && pecl install imagick \
    && docker-php-ext-enable imagick


# Install Princexml
RUN PRINCE_FILE=prince-15-linux-generic-$(arch)$(if [ $(arch) = "aarch64" ]; then echo '-musl'; fi;) \
    && curl -O https://www.princexml.com/download/$PRINCE_FILE.tar.gz \
    && tar -xzf $PRINCE_FILE.tar.gz \
    && sh $PRINCE_FILE/install.sh \
    && rm -rf $PRINCE_FILE $PRINCE_FILE.tar.gz

WORKDIR /var/app
