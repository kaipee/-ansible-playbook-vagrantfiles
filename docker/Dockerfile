# Start from the Ubuntu base image
FROM ubuntu:latest

# Avoid prompts from apt
ENV DEBIAN_FRONTEND=noninteractive

# Update and install SSH
RUN apt-get update && apt-get install -y openssh-server

# Setup SSH service
RUN mkdir /var/run/sshd

# Set root password to 'root' (or another password of your choice)
RUN echo 'root:root' | chpasswd

# Permit root login via SSH
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

# Expose port 22 for SSH access
EXPOSE 22

# Start SSH when the container launches
CMD ["/usr/sbin/sshd", "-D"]

# Create image with systemd and boot like a real environment.
RUN apt-get install -y systemd systemd-sysv dbus dbus-user-session
RUN printf "systemctl start systemd-logind" >> /etc/profile

ENTRYPOINT ["/sbin/init"]
