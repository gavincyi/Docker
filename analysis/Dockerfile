# Copyright (c) Gavin Chan

FROM jupyter/scipy-notebook

MAINTAINER Gavin Chan <gavincyi at gmail dot com>

USER jovyan

# Environment
ENV VISUAL vim
ENV EDITOR ${VISUAL}

# Git environment setup
RUN git config --global user.email "gavincyi@gmail.com"
RUN git config --global user.name "Gavin Chan"

# Clone project
RUN git clone https://github.com/gavincyi/HkexStockPicker.git


