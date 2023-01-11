FROM php:7.4-fpm-alpine

ENV NODE_VERSION 18.13.0


# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# Install php modules
RUN apk add libzip-dev libxml2-dev libpng-dev autoconf imagemagick-dev imagemagick && \
    docker-php-ext-install zip soap gd mysqli \
    && pecl install imagick \
    && docker-php-ext-enable imagick


# Install Princexml
RUN PRINCE_FILE=prince-15-linux-generic-$(arch)$(if [ $(arch) = "aarch64" ]; then echo '-musl'; fi;) \
    && curl -O https://www.princexml.com/download/$PRINCE_FILE.tar.gz \
    && tar -xzf $PRINCE_FILE.tar.gz \
    && sh $PRINCE_FILE/install.sh \
    && rm -rf $PRINCE_FILE $PRINCE_FILE.tar.gz

RUN apk add binutils-gold \
        g++ \
        gcc \
        gnupg \
        libgcc \
        linux-headers \
        make \
        python3 \
    && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION.tar.xz" \
    && tar -xf "node-v$NODE_VERSION.tar.xz" \
    && cd "node-v$NODE_VERSION" \
    && ./configure \
    && make -j$(getconf _NPROCESSORS_ONLN) V= \
    && make install \
    && cd .. \
    && rm -Rf "node-v$NODE_VERSION"

WORKDIR /var/app
