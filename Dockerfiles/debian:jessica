FROM debian:jessie

RUN buildDeps=" \
        nano unzip bzip2 \
        ca-certificates curl librecode0 libsqlite3-0 libxml2 \
        autoconf file g++ gcc libc-dev make pkg-config re2c \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libxml2-dev libc-client2007e-dev  \
        libssl-dev libbz2-dev libxslt1-dev libcurl4-openssl-dev \
        libmemcached-dev libmagick++-dev libkrb5-dev  libicu-dev \
        libpq-dev libtidy-dev libgearman-dev libev-dev \
		libreadline6-dev \
		librecode-dev \
		libsqlite3-dev \
	" \
	&& set -x \
    && apt-get update && apt-get install -y $buildDeps --force-yes  --no-install-recommends && apt-get autoremove -y && apt-get clean -y  \
    && ln -s `find /usr/lib/x86_64-linux-gnu/ImageMagick-*/bin* -type d`/* /usr/local/bin/ \
    && rm -rf /var/lib/apt/lists/* \

CMD ["/bin/bash"]
