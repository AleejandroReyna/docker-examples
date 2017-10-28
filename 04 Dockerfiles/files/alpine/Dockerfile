#establece la imagen a utilizar
FROM alpine:latest

#Establece información sobre nosotros
LABEL Author aleejandroreyna

#actualiza los repos
RUN apk update

#actualiza el os
RUN apk upgrade

#instala los programas a utilizar
RUN apk add openssh vim sudo bash

#crea el grupo de usuarios
RUN addgroup alejandro

#crea el usuario y le asigna el bash por defecto
RUN adduser -s /bin/bash -G alejandro alejandro -D

#crear contraseña para el usuario
RUN echo alejandro:alejandro | chpasswd

#Agrega al usuario al grupo wheel
RUN sed -ri 's/(wheel:x:10:root)/\1,alejandro/' /etc/group

#Agrega permisos sudo a todos los usuarios del grupo wheel
RUN sed -ri 's/# %wheel ALL=\(ALL\) ALL/%wheel ALL=\(ALL\) ALL/' /etc/sudoers

#Coloca para el usuario root la bash
RUN sed -ri 's;^(root:x:0:0:root:/root:)/bin/ash;\1/bin/bash;' /etc/passwd

#agrega el directorio sshd
RUN mkdir /var/run/sshd

#modifica el permiso para el login del usuario root
RUN sed -ri 's/^#PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config

#Agregar las ssh-key

#Variable de entorno para realizar un comando (Sin espacios, importante)

ENV KEYGEN="ssh-keygen -b 2048 -t rsa -f"

RUN $KEYGEN /etc/ssh/ssh_host_rsa_key -q -N "" 
RUN $KEYGEN /etc/ssh/ssh_host_dsa_key -q -N ""
RUN $KEYGEN /etc/ssh/ssh_host_ecdsa_key -q -N ""
RUN $KEYGEN /etc/ssh/ssh_host_ed25519_key -q -N ""

#Expone el puerto a utilizar

EXPOSE 22

#Comando que ejecutará docker para crear el contenedor
CMD [ "/usr/sbin/sshd", "-D" ]