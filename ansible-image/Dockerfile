FROM ubuntu:16.04

RUN apt-get update && apt-get install -y openssh-server vim
RUN mkdir /var/run/sshd
RUN echo "root:Omisoka1231" | chpasswd
RUN sed -i "s/PermitRootLogin prohibit-password/PermitRootLogin yes/" /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed "s@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g" -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

# FOR Ansible
RUN apt-get install -y software-properties-common
RUN apt-add-repository --yes --update ppa:ansible/ansible
RUN apt-get install -y ansible

RUN apt-get -y install python

WORKDIR /root/.ssh
COPY ./id_ecdsa .
COPY ./id_ecdsa.pub .

WORKDIR /ansible

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]