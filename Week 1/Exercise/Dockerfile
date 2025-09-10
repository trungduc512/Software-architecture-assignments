FROM ubuntu:latest

RUN apt update && apt install -y openssh-server
RUN apt install -y tightvncserver
RUN echo 'root:123456' | chpasswd
EXPOSE 22
RUN sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/' /etc/ssh/sshd_config
RUN mkdir /var/run/sshd
CMD ["/usr/sbin/sshd", "-D"]
RUN apt install -y xfce4 xfce4-goodies
RUN apt install -y dbus-x11
# Set VNC password non-interactively
RUN mkdir -p /root/.vnc && \
    echo "123456" | vncpasswd -f > /root/.vnc/passwd && \
    chmod 600 /root/.vnc/passwd
# Create xstartup script to start XFCE4
RUN echo -e '#!/bin/bash\nxrdb $HOME/.Xresources\nstartxfce4 &' > /root/.vnc/xstartup \
    && chmod +x /root/.vnc/xstartup
