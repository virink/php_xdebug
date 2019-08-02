FROM php:7.4-rc-apache

LABEL Author="Virink <virink@outlook.com>" NAME="PHP 7.4 with xdebug 2.8.0beta1"
MAINTAINER Virink@CTFHUB <virink@outlook.com>

RUN sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list \
    && sed -i 's/archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list \
    && sed -i '/security/d' /etc/apt/sources.list \
    && apt-get update -y

# XDebug
RUN pecl install xdebug-2.8.0beta1 \
    && docker-php-ext-enable xdebug \
    && { while true; do \
        echo "xdebug.remote_enable=1"; \
        echo "xdebug.remote_port=9000"; \
        echo "xdebug.remote_connect_back=1"; \
        break; \
    done } >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Base Exts
RUN apt install -y zlib1g-dev libpng-dev libjpeg-dev \
    && docker-php-ext-install gd

# Apache2 rewrite
RUN a2enmod rewrite

EXPOSE 9000
EXPOSE 80