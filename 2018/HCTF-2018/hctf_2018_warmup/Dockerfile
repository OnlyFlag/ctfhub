FROM nimmis/apache:14.04

# disable interactive functions
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
apt-get install -y php5 libapache2-mod-php5  \
php5-fpm php5-cli php5-mysqlnd php5-pgsql php5-sqlite php5-redis \
php5-apcu php5-intl php5-imagick php5-mcrypt php5-json php5-gd php5-curl && \
php5enmod mcrypt && \
rm -rf /var/lib/apt/lists/* && \
cd /tmp && curl https://getcomposer.org/installer -o test.php && php test.php && mv composer.phar /usr/local/bin/composer

COPY run.sh /
RUN chmod 755 /run.sh
COPY ffffllllaaaagggg /
COPY source.php /var/www/html
COPY hint.php /var/www/html
COPY index.php /var/www/html
COPY code.php /var/www/html

RUN rm /var/www/html/index.html

EXPOSE 80
