FROM public.ecr.aws/docker/library/php:8.1.8-fpm
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ENV JWT_ALGO="HS256"
ENV PROJECT_DIR='/laravel-project'
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV COMPOSER_HOME='/composer'
ENV PHP_UID=1000
ENV PHP_GID=1000
ENV DOCKER_USER='www-data'
ENV APPLICATION_LOG_DIR=/var/log/bizmates/laravel-project
ENV APP_ENV="dev"
ARG APP_ENV

WORKDIR $PROJECT_DIR

RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer
RUN apt-get update \
&& apt-get install -y \
git \
zip \
unzip \
vim

RUN apt-get update \
    && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo_mysql pdo_pgsql

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
COPY ["./docker/${APP_ENV}/php/php-fpm.conf", "/usr/local/etc/php-fpm.conf"]
COPY ["./docker/${APP_ENV}/php/conf.d/uploads.ini", "$PHP_INI_DIR/conf.d/uploads.ini"]
COPY ["./docker/${APP_ENV}/php/docker-entrypoint.sh", "/"]
RUN chmod +x /docker-entrypoint.sh

COPY ["./", "./"]

RUN composer install

EXPOSE 9000

ENTRYPOINT ["/docker-entrypoint.sh"]
