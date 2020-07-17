# image
FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update -y \
	&& apt upgrade -y

# add node 14 
RUN apt install -y openssh-server build-essential git curl \
	&& curl -sL https://deb.nodesource.com/setup_14.x | bash - \
	&& apt install -y nodejs

RUN npm i -g yarn

# setup ssh
RUN mkdir /var/run/sshd
RUN echo 'root:YOURPASSWORDHERE' | chpasswd

RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# exposed ports
EXPOSE 22 80 8080

# create workspace dir
RUN mkdir /workspace

CMD ["/usr/sbin/sshd", "-D"]
