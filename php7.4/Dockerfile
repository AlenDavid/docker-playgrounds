FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update -y \
    && apt upgrade -y \
    && apt install openssh-server build-essential git curl zsh software-properties-common -y \
    && add-apt-repository ppa:ondrej/php -y \
    && apt install php7.4 php-pear php7.4-curl php7.4-dev php7.4-gd php7.4-mbstring php7.4-zip php7.4-mysql php7.4-xml -y

RUN sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)" \
    && chsh -s $(which zsh) \
    && git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

RUN mkdir /var/run/sshd
RUN echo 'root:YOURPASSWORDHERE' | chpasswd

RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN git config --global user.email davidalen51@gmail.com \
    git config --global user.name "David Alen"


# exposed ports
EXPOSE 22 80 8080

# create workspace dir
RUN mkdir /workspace

CMD ["/usr/sbin/sshd", "-D"]