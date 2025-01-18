# Using Official Redhat 9.5 UBI Image #
FROM redhat/ubi9:9.5

# Labels #
LABEL OS="Red Hat Enterprise Linux 9.5 (Plow)"
LABEL Image="Red Hat Universal Base Image 9"
LABEL Maintainer="Mahesh Kumar Gupta"
LABEL Email="mahesh.gupta1804@gmail.com"

# Update image, install openssh, sudo & python3 #
RUN <<EOF
yum install -y openssh-server
yum install -y sudo
yum install -y python3.12
yum install -y iputils
EOF

# Create a user, group and set a password #
RUN <<EOF
groupadd -g 1001 admin
useradd -rm -d /home/admin -s /bin/bash -g admin -u 1001 admin
EOF

# Create dir & add authorized_keys #
RUN mkdir -p /home/admin/.ssh
RUN chown admin:admin /home/admin/.ssh

# Generate SSH host keys
RUN ssh-keygen -A

# WORKDIR /home/admin/.ssh/
COPY authorized_keys /home/admin/.ssh/
RUN chown admin:admin /home/admin/.ssh/authorized_keys

# Create sudo entry for admin user #
# WORKDIR /etc/sudoers.d/
COPY admin /etc/sudoers.d/


# Configure SSH #
RUN mkdir /var/run/sshd && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "export VISIBLE=now" >> /etc/profile

# Expose the SSH port #
EXPOSE 22

# Start the SSH service
CMD ["/usr/sbin/sshd", "-D"]
