FROM ubuntu:18.04
LABEL name="HIWC App"
LABEL version="2.0"

ENV DEBIAN_FRONTEND noninteractive
# System env variables.
ENV DRUSH_VERSION 8.3.0
ENV VAR_DUMPER_VERSION 4.3.3
ENV GOSU_VERSION 1.11
ENV TIMEZONE "Europe/Madrid"
ENV PROJECT_DIR=/var/www/html

# Install packages.
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  curl \
  dump \
  rsyslog \
  mysql-client \
  libpng-dev \
  libjpeg-dev \
  libxml2-dev \
  git \
  zip \
  unzip \
  vim \
  libicu-dev \
  libssl-dev \
  libimage-exiftool-perl \
  openssl \
  php \
  php-pear \
  php-dev \
  php-soap \
  php-gd \
  php-mbstring \
  php-pdo \
  php-zip \
  php-intl \
  php-mysql \
  php-curl \
  php-json \
  apache2 \
  ca-certificates \
  && echo "$TIMEZONE" > /etc/timezone \
  && rm -f /etc/localtime \
  && dpkg-reconfigure -f noninteractive tzdata \
  && apt-get autoremove -y \
  && apt-get autoclean -y \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install composer, drush and other tools.
ENV COMPOSER_HOME /composer-libs
RUN mkdir /composer-libs \
  && curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer \
  && composer global require symfony/var-dumper:$VAR_DUMPER_VERSION \
  && chown -R www-data:www-data /composer-libs \
  && curl -fSL "https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar" -o /usr/bin/drush \
  && chmod +x /usr/bin/drush \
  && drush @none dl registry_rebuild-7.x-2.5 \
  && echo "PS1='\[\033[1;36m\]\u\[\033[1;31m\]@\[\033[1;32m\]\h:\[\033[1;35m\]\w\[\033[1;31m\]\$\[\033[0m\] '" >> /etc/bash.bashrc \
  && echo "export TERM=xterm" >> /etc/bash.bashrc \
  && echo "umask 000" >> /etc/bash.bashrc \
  && curl -fSL "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" -o /usr/bin/gosu

## Configure PHP and Apache.
COPY config/docker/php/*.ini /etc/php/7.2/apache2/conf.d/
COPY config/docker/apache/config/*.conf /etc/apache2/conf-enabled/
RUN rm -rf /etc/apache2/sites-enabled/*

# Enable apache rewrite.
RUN a2enmod rewrite

# Enable apache default site
RUN rm -f /etc/apache2/sites-enabled/000-default.conf
COPY config/docker/apache/sites/000-default.conf /etc/apache2/sites-available/
RUN a2ensite 000-default

# Configure apache
RUN a2enmod rewrite
RUN chown -R www-data:www-data /var/www/html

ENV APACHE_RUN_USER  www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR   /var/log/apache2
ENV APACHE_PID_FILE  /var/run/apache2/apache2.pid
ENV APACHE_RUN_DIR   /var/run/apache2
ENV APACHE_LOCK_DIR  /var/lock/apache2
ENV APACHE_LOG_DIR   /var/log/apache2

RUN mkdir -p $APACHE_RUN_DIR
RUN mkdir -p $APACHE_LOCK_DIR
RUN mkdir -p $APACHE_LOG_DIR

EXPOSE 80

CMD ["/usr/sbin/apache2", "-D",  "FOREGROUND"]

WORKDIR $PROJECT_DIR
