# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM sechiro/pyspark-notebook

MAINTAINER Jupyter Project <jupyter@googlegroups.com>

USER root

# RSpark config
ENV R_LIBS_USER $SPARK_HOME/R/lib

# R pre-requisites
RUN yum -y update && \
    yum -y install \
    fonts-dejavu \
    gcc-gfortran \
    gcc \
    glibc \
    e2fsprogs \
    krb5-libs \
    openssl

USER $NB_USER

# R packages
# Pin r-base to a specific build number for https://github.com/jupyter/docker-stacks/issues/210#issuecomment-246081809
RUN conda config --add channels r && \
    conda install --quiet --yes \
    'r-base=3.3.1 1' \
    'r-irkernel=0.6*' \
    'r-ggplot2=2.1*' \
    'r-rcurl=1.95*' && conda clean -tipsy

# Apache Toree kernel
ENV PYSPARK_SUBMIT_ARGS "--master local[2] pyspark-shell"
COPY msodbcsql-13.0.0.0.tar.gz /tmp
RUN pip --no-cache-dir install toree==0.1.0.dev7
RUN jupyter toree install --user
