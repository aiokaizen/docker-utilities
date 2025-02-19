FROM ubuntu:24.04

# Install necessary packages including SSH and GPG (GnuPG -- Pretty Good Privacy)
RUN apt update && \
    apt install -y openssh-server gnupg

RUN mkdir /var/run/sshd && \
    useradd -m -s /bin/bash sshduser && \
    echo "sshduser:admin@123" | chpasswd && \
    echo "PermitRootLogin yes" >> /etc/ssh/sshd_config && \
    echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config

# Expose SSH port
EXPOSE 22

# Start SSH service
CMD ["/usr/sbin/sshd", "-D"]

