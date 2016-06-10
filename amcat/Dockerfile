# Amcat version 1.4.1

# VERSION 20160608_1

FROM phusion/baseimage:latest

MAINTAINER Rene Nederhand <rene@cogfor.com>

# Set correct environment variables.
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

#RUN apt-get update && apt-get -y install antiword unrtf rabbitmq-server python-pylibmc python-virtualenv python-dev python-pip postgresql postgresql-contrib postgresql-server-dev-9.3 libxml2-dev libxslt-dev python-pdfminer graphviz pspp python-lxml python-amqplib python-psycopg2 python-requests python-pygments git libmemcached-dev

RUN apt-get update && apt-get -y install antiword unrtf rabbitmq-server python-pip python-dev libxml2-dev libxslt-dev lib32z1-dev postgresql postgresql-server-dev-9.3 postgresql-contrib-9.3 python-virtualenv git graphviz

# Install R
RUN sudo sh -c "echo 'deb https://cran.rstudio.com/bin/linux/ubuntu trusty/' > /etc/apt/sources.list.d/r-cran-trusty.list"
RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
RUN sudo apt-get update 
RUN sudo apt-get -y install r-base r-base-dev

# Install AmCAT
RUN git clone -b release-3.4 https://github.com/amcat/amcat.git
#RUN git clone https://github.com/amcat/amcat.git

# Create Python VirtualEnv
#RUN virtualenv ~/amcat-env
#RUN /bin/bash ~/amcat-env/bin/activate
RUN pip install -r amcat/requirements.txt

# Install logstash logging support (optional)
RUN pip install python-logstash

ENV PYTHONPATH $PYTHONPATH:$HOME/amcat
ENV AMCAT_ES_LEGACY_HASH N

WORKDIR /amcat

# Collecting static files
RUN apt-get install -y nodejs-legacy npm
RUN npm install -g bower
RUN echo '{ "allow_root": true }' > /root/.bowerrc
RUN bower install

# Setting up the database
#RUN python -m amcat.manage migrate

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 
