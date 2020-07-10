FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update -y \
    && apt upgrade -y \
    && apt install php7.4 openssh-server build-essential git curl -y

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

# setup ssh
RUN mkdir /var/run/sshd

RUN echo 'root:123qweasd' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# exposed ports
EXPOSE 22 80 8080 1900-2000 20000-29999

# create workspace dir
RUN mkdir /workspace

CMD ["/usr/sbin/sshd", "-D"]