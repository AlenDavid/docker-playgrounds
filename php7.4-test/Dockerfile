FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update -y \
  && apt upgrade -y 

RUN apt install build-essential git curl zsh software-properties-common default-mysql-client default-mysql-server -y 
RUN add-apt-repository ppa:ondrej/php -y
RUN apt install php7.4 php-pear php7.4-curl php7.4-dev php7.4-gd php7.4-mbstring php7.4-zip php7.4-mysql php7.4-xml -y
RUN apt install php7.4-mysql php7.4-curl php7.4-json php7.4-cgi php7.4-xsl php7.4-mbstring php7.4-dom php7.4-zip -y

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && php -r "unlink('composer-setup.php');"

ENV MYSQL_ROOT_PASSWORD=insertpasswordhere
ENV MYSQL_HOST=127.0.0.1

RUN service mysql start
