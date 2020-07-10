FROM ubuntu:20.04

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:YOURPASSWORDHERE' | chpasswd

RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]