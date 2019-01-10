FROM php:7.0-fpm-alpine

LABEL Author="Virink <virink@outlook.com>"

COPY www /www/
COPY config /config/
COPY startcmd /startcmd/
COPY flag.txt /etc/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories \
    && apk update \
    && apk add nginx libxml2-dev \
    && mkdir /run/nginx \
    && cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini \
    && sed -i -e 's/display_errors.*/display_errors = Off/' /usr/local/etc/php/php.ini \
    # configure file
    && mv /startcmd/docker-php-entrypoint /usr/local/bin/docker-php-entrypoint \
	&& chmod u+x /usr/local/bin/docker-php-entrypoint \
    && mv /config/nginx.conf /etc/nginx/nginx.conf \
    && mv /config/vhost.nginx.conf /etc/nginx/conf.d/default.conf \
    # www
    && mv /www/html/* /var/www/html/ \
	&& mv /www/avatar.gif /var/www/ \
	&& mv /www/read_secret /var/www/ \
	&& chmod -R 755 /var/www/ \
    && chmod -R -w /var/www/html \
    && chown -R www-data:www-data /var/www/html \
    # clear
    && rm -rf /tmp/* \
    && rm -rf /etc/apk

EXPOSE 80

VOLUME ["/var/log/nginx"]

CMD ["/bin/sh", "-c", "/usr/local/bin/docker-php-entrypoint"]