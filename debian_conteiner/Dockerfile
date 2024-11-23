FROM debian:latest

#install system tools
RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y openssh-server sudo wireless-tools python3-pip iputils-ping net-tools

#creating user, system directories
RUN mkdir /var/run/sshd
RUN useradd -m -d /home/tony -s /bin/bash tony
RUN echo "tony:kali" | chpasswd
RUN usermod -aG sudo tony

#SSH settings
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin no/' /etc/ssh/sshd_config
RUN echo "AllowUsers tony" >> /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config
EXPOSE 22

#install software tools
RUN apt-get install -y vim curl python3 wget

#installing Guacamole
#RUN apt-get install -y build-essential libcairo2-dev libjpeg-dev libpng-dev libtool-bin libossp-uuid-dev libvncserver-dev freerdp2-dev libpango1.0-dev libssh2-1-dev libtelnet-dev libssl-dev libpulse-dev libvorbis-dev libwebp-dev libavcodec-dev libavutil-dev libavformat-dev libavutil-dev libswscale-dev libavfilter-dev libavdevice-dev
#RUN wget https://apache.org/dyn/closer.cgi?action=download&filename=guacamole/1.5.0/source/guacamole-server-1.5.0.tar.gz
#RUN tar -xvzf guacamole-server-1.5.0.tar.gz
#RUN cd guacamole-server-1.5.0

#RUN ./configure --with-init-dir=/etc/init.d
#RUN make
#RUN make install
#RUN ldconfig

CMD ["/usr/sbin/sshd", "-D"]
