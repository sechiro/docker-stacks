# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.

FROM sechiro/base-notebook

MAINTAINER Jupyter Project <jupyter@googlegroups.com>

USER root

# Install all OS dependencies for fully functional notebook server
RUN yum update -y && yum install -y \
    git \
    vim \
    jed \
    emacs \
    gcc \
    python-dev \
    unzip \
    libsm6 \
    pandoc \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-generic-recommended \
    libxrender1 \
    inkscape 

# Switch back to jovyan to avoid accidental container runs as root
USER $NB_USER
