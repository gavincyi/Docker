# Copyright (c) Gavin Chan

FROM centos:7

MAINTAINER Gavin Chan <gavincyi at gmail dot com>

USER root

RUN mkdir /root/Downloads

# Environment
ENV VISUAL vim
ENV EDITOR ${VISUAL}
ENV DWLD /root/Downloads

# Expose port for ssh
EXPOSE 22

# Packages

RUN cd /root/Downloads
RUN yum install -y wget
RUN wget https://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-6.noarch.rpm -P ${DWLD} && \
    wget http://rpms.famillecollet.com/enterprise/remi-release-7.rpm -P ${DWLD}
RUN rpm -Uvh ${DWLD}/remi-release-7*.rpm ${DWLD}/epel-release-7*.rpm
RUN yum groupinstall -y "Development tools"
RUN yum install -y zlib-devel
RUN yum install -y which
RUN yum install -y python-devel
RUN yum install -y bzip2-devel-1.0.6-13.el7.x86_64

# Install POCO
RUN cd /root/Downloads && \
    wget http://pocoproject.org/releases/poco-1.7.2/poco-1.7.2.tar.gz && \
    gunzip poco-1.7.2.tar.gz && \
    tar -xvf ${DWLD}/poco-1.7.2.tar && \
	cd poco-1.7.2 && \
    ./configure && \
	make && \
    make install

# Install fix8
RUN cd /root/Downloads && \
	wget https://github.com/fix8/fix8/archive/1.3.4.tar.gz && \
    gunzip 1.3.4.tar.gz && \
    tar -xvf 1.3.4.tar && \
    cd fix8-1.3.4/ && \
    ./bootstrap && \
    ./configure && \
    make && \
    make install

# Install boost
RUN cd /root/Downloads && \
	wget http://sourceforge.net/projects/boost/files/boost/1.60.0/boost_1_60_0.tar.bz2/download -O boost_1_60_0.tar.bz2 && \
    bunzip2 boost_1_60_0.tar.bz2 && \
    tar xvf boost_1_60_0.tar  && \
    cd boost_1_60_0 && \
    ./bootstrap.sh && \
    ./b2

# Git environment setup
RUN git config --global user.email "gavincyi@gmail.com"
RUN git config --global user.name "Gavin Chan"

# Install SSHD
RUN yum install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd
RUN ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N ""
RUN ssh-keygen -f /etc/ssh/ssh_host_ecdsa_key -N ""
RUN ssh-keygen -f /etc/ssh/ssh_host_ed25519_key -N ""
CMD ["/usr/sbin/sshd", "-D"]

