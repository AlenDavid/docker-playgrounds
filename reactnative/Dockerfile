# image
FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update
RUN apt install -y openssh-server build-essential nodejs git curl

# add node 14 
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -

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