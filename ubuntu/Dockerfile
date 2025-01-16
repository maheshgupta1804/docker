# Buiding an Ubuntu Image from Version 24.04 #
FROM ubuntu:24.04

# Labels #
LABEL OS="Ubuntu-24.04"
LABEL Maintainer="Mahesh Gupta"
LABEL Email="mahesh.gupta1804@gmail.com"

# Update image & Install openssh #
RUN <<EOF
apt update -y
apt install -y openssh-server
EOF

# Create a user, group and set a password #
RUN <<EOF
groupadd -g 1001 admin
useradd -rm -d /home/admin -s /bin/bash -g admin -u 1001 admin
EOF

# Create dir & add authorized_keys
RUN mkdir -p /home/admin/.ssh
RUN chown admin:admin /home/admin/.ssh

WORKDIR /home/admin/.ssh/
COPY authorized_keys .
RUN chown admin:admin authorized_keys
WORKDIR /

# Configure SSH
RUN mkdir /var/run/sshd && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "export VISIBLE=now" >> /etc/profile

# Expose the SSH port
EXPOSE 22

# Start the SSH service
CMD ["/usr/sbin/sshd", "-D"]
