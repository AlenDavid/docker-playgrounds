FROM ubuntu:20.04

RUN apt update -y \
    && apt upgrade -y \
    && apt install software-properties-common -y \
    && add-apt-repository ppa:ondrej/php -y \
    && apt update -y \
    && apt install php7.4.7 -y

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

EXPOSE 22 80

