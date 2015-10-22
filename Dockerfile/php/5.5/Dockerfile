FROM php:5.5-fpm
MAINTAINER Zhu yajie <xcoolcc@gmail.com>

RUN buildDeps=" \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libxml2-dev libc-client2007e-dev  \
        libssl-dev libbz2-dev libxslt1-dev libcurl4-openssl-dev \
        libmemcached-dev libmagick++-dev libkrb5-dev  libicu-dev \
        libpq-dev libtidy-dev libgearman-dev libev-dev \
	" \
	&& set -x \
    && apt-get update && apt-get install -y nano unzip  $buildDeps --force-yes  --no-install-recommends  \
    && ln -s `find /usr/lib/x86_64-linux-gnu/ImageMagick-*/bin* -type d`/* /usr/local/bin/

RUN curl -L -o phptrace.zip https://github.com/Qihoo360/phptrace/archive/master.zip && unzip phptrace.zip &&  cd phptrace-master/extension && phpize && ./configure && make && make install && cd ../cmdtool && make && cp phptrace /usr/local/bin/  && cd ../.. && rm -fr phptrace* \
    && curl -L -o xhprof.zip https://github.com/phacility/xhprof/archive/master.zip && unzip xhprof.zip && cd xhprof-master/extension && phpize && ./configure && make && make install && cd - && rm -fr xhprof* \
    && curl -L -o cphalcon.zip https://github.com/phalcon/cphalcon/archive/master.zip && unzip cphalcon.zip && cd cphalcon-master/build/64bits && phpize && ./configure && make && make install && cd - && rm -fr cphalcon* \
    && curl -L -o phpredis.zip https://github.com/phpredis/phpredis/archive/master.zip && unzip phpredis.zip && cd phpredis-master && phpize && ./configure && make && make install && cd - && rm -fr phpredis* \
    && pecl install ev imagick gearman solr igbinary mongo memcache memcached xdebug swoole \
    && docker-php-ext-configure imap  --with-imap --with-imap-ssl --with-kerberos \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --enable-gd-native-ttf \
    && docker-php-ext-configure hash --with-mhash \
    && docker-php-ext-install tidy  tokenizer wddx xmlrpc  xsl opcache \
       bz2 bcmath curl calendar dba gd exif ftp gettext imap intl mbstring mcrypt mysqli pcntl pdo_mysql pdo_pgsql pgsql  sockets shmop  sysvsem soap sysvmsg  sysvshm   zip \
    && docker-php-ext-enable trace phalcon redis xhprof solr igbinary mongo memcache memcached xdebug swoole opcache ev gearman imagick \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false $buildDeps \
    && rm -rf /var/lib/apt/lists/* \
CMD ["php-fpm"]
