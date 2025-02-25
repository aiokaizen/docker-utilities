FROM ubuntu:24.04

# Define build arguments
ARG SSH_USER_PASSWORD
ARG SSH_ADMIN_PASSWORD

# Environment variables
ENV SSH_USER_PASSWORD=${SSH_USER_PASSWORD}

# Install necessary packages including SSH and GPG (GnuPG -- Pretty Good Privacy)
RUN apt update && \
    apt install -y openssh-server gnupg sudo

RUN mkdir /var/run/sshd && \
    useradd -m -s /bin/bash sshuser && \
    echo "PermitRootLogin yes" >> /etc/ssh/sshd_config && \
    echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config

RUN useradd -m -s /bin/bash sshadmin -G sudo

RUN echo "sshuser:${SSH_USER_PASSWORD}" | chpasswd
RUN echo "sshadmin:${SSH_ADMIN_PASSWORD}" | chpasswd

# Expose SSH port
EXPOSE 22

# Start SSH service
CMD ["/usr/sbin/sshd", "-D"]

