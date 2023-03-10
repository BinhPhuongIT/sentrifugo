FROM php:7.1.12-apache
COPY /php/php.ini /usr/local/etc/php/

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libxml2-dev \
        apache2-dev \
        libssl-dev \
        libcurl4-gnutls-dev \
        libedit-dev \
        librecode-dev \
        zlib1g-dev \
        unzip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure calendar --enable-calendar \
    && docker-php-ext-install calendar \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-configure readline --with-readline \
    && docker-php-ext-install readline \
    && docker-php-ext-configure recode --with-recode \
    && docker-php-ext-install recode \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-configure zip --enable-zip \
    && docker-php-ext-install zip

ADD start.sh /start.sh
RUN chmod +x /start.sh

ADD Sentrifugo.zip /Sentrifugo.zip
RUN unzip /Sentrifugo.zip -d / && rm -rfv /Sentrifugo.zip && mv -v /Sentrifugo_3.2 /var/www/html
RUN chown -R www-data:www-data /var/www/html/

RUN a2enmod rewrite
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-server && rm -rf /var/lib/apt/lists/*

CMD /start.sh