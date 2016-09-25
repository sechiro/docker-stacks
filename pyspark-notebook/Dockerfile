# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM sechiro/scipy-notebook

MAINTAINER Jupyter Project <jupyter@googlegroups.com>

USER root

# Spark dependencies
ENV APACHE_SPARK_VERSION 1.6.1
RUN yum -y update && \
    yum install -y java-1.7.0-openjdk-headless
RUN cd /tmp && \
        wget -q http://d3kbcqa49mib13.cloudfront.net/spark-${APACHE_SPARK_VERSION}-bin-hadoop2.6.tgz && \
        echo "09f3b50676abc9b3d1895773d18976953ee76945afa72fa57e6473ce4e215970 *spark-${APACHE_SPARK_VERSION}-bin-hadoop2.6.tgz" | sha256sum -c - && \
        tar xzf spark-${APACHE_SPARK_VERSION}-bin-hadoop2.6.tgz -C /usr/local && \
        rm spark-${APACHE_SPARK_VERSION}-bin-hadoop2.6.tgz
RUN cd /usr/local && ln -s spark-${APACHE_SPARK_VERSION}-bin-hadoop2.6 spark

# Mesos dependencies
# Currently, Mesos is not available from Debian Jessie.
# So, we are installing it from Debian Wheezy. Once it
# becomes available for Debian Jessie. We should switch
# over to using that instead.
RUN rpm -Uvh http://repos.mesosphere.io/el/7/noarch/RPMS/mesosphere-el-repo-7-1.noarch.rpm && yum -y install  mesos marathon chronos mesosphere-zookeeper 

# Spark and Mesos config
ENV SPARK_HOME /usr/local/spark
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.9-src.zip
ENV MESOS_NATIVE_LIBRARY /usr/local/lib/libmesos.so
ENV SPARK_OPTS --driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info

USER $NB_USER
