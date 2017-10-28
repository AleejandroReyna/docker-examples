FROM debian

LABEL Author aleejandroreyna

RUN apt-get -y update && apt-get -y upgrade

RUN apt-get install -y sudo vim openssh-server 

RUN adduser alejandro

RUN echo alejandro:alejandro | chpasswd

RUN sed -ri 's/(sudo:x:27)/\1:alejandro/' /etc/group

RUN sed -ri 's/# %sudo ALL=\(ALL\) ALL/%sudo ALL=\(ALL\) ALL/' /etc/sudoers

RUN mkdir /var/run/sshd

RUN sed -ri 's/^#PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config

EXPOSE 22

CMD [ "/usr/sbin/sshd", "-D" ]