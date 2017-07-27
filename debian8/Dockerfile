# Use debian8 based node v6 upstream image
FROM docker.io/node:6

RUN apt-get update && \
    apt-get install --no-install-recommends --no-install-suggests -y git wget curl ca-certificates libapache2-mod-xsendfile imagemagick ghostscript php5-fpm php5-cli php5-curl php5-apcu php5-gd php5-imap php5-intl php5-ldap php5-mcrypt php5-mysql php5-pgsql php5-sqlite php5-redis php5-igbinary php5-imagick php5-pspell php5-recode php5-xmlrpc php5-memcached php-http-request2 && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/www/html/*

# Install php mongo extension
RUN apt-get update && \
    apt-get install --no-install-recommends --no-install-suggests -y php5-dev re2c make && \
    pecl install mongo && \
    echo "extension = mongo.so" > /etc/php5/mods-available/mongo.ini && \
    apt-get --purge autoremove -y php5-dev re2c make && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN php5enmod mongo

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install grunt
RUN set -x && \
  npm install -g grunt && \
  ln -s /usr/bin/nodejs /usr/bin/node && \
  npm cache clean

RUN mkdir /root/.ssh && \
  chmod 700 /root/.ssh && \
  echo "Host *\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config

WORKDIR /var/www/html
