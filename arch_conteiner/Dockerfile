FROM archlinux:latest

#installing system utils
RUN pacman -Syu --noconfirm && pacman -S --noconfirm base base-devel vim
RUN pacman -S --noconfirm openssh sudo python3 python-pip iputils net-tools 

#creating users
RUN useradd -m -d /home/tony -s /bin/bash tony
RUN echo "tony:kali" | chpasswd
RUN usermod -aG wheel tony
RUN echo "%wheel ALL=(ALL) ALL" >> /etc/sudoers

#SSH settings
RUN mkdir /run/sshd
RUN ssh-keygen -A
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin no/' /etc/ssh/sshd_config
RUN echo "AllowUsers tony" >> /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]