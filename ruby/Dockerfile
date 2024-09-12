FROM rockylinux:8 as base

# Upgrade the system and install necessary packages using dnf
RUN dnf -y upgrade && \
    dnf -y install epel-release && \
    dnf -y install supervisor git gcc gcc-c++ zip unzip wget tar make \
    bzip2 openssl-devel bzip2-devel libffi-devel readline-devel

# Install Ruby, Jekyll, and set up powertools for Ruby installation
RUN dnf config-manager --set-enabled powertools && \
    dnf module reset ruby -y && \
    dnf module install ruby:3.0 -y && \
    dnf install -y ruby-devel && \
    gem install bundler && \
    gem install jekyll

# Add supervisor configuration for SSHD
ADD sshd.ini /etc/supervisord.d/sshd.ini

# Generate SSH keys and set proper permissions
RUN /usr/bin/ssh-keygen -A && \
    chmod 755 /etc/supervisord.d/sshd.ini

# Set the working directory
WORKDIR /var/www/jekyllrb
