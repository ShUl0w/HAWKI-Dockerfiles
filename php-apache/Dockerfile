FROM alpine:latest as build

RUN apk update && apk add git

WORKDIR /tmp

RUN git clone https://github.com/HAWK-Digital-Environments/HAWKI.git 

FROM php:apache

RUN apt update && export DEBIAN_FRONTEND=noninteractive && apt -y install --no-install-recommends cron libldap2-dev

RUN docker-php-ext-configure ldap
RUN docker-php-ext-install ldap

RUN echo 'date.timezone = Europe/Amsterdam' >> /usr/local/etc/php/conf.d/docker-php-datetimezone.ini;
RUN echo 'max_execution_time = 300' >> /usr/local/etc/php/conf.d/docker-php-maxexectime.ini;
RUN echo 'max_input_vars = 3000' >> /usr/local/etc/php/conf.d/docker-php-maxinputvars.ini;

RUN a2enmod rewrite
RUN a2enmod headers

COPY --from=build /tmp/HAWKI /var/www/html
COPY .env.example /var/www/html/private/.env

RUN chmod +x /var/www/html/composer_install.sh && /var/www/html/composer_install.sh