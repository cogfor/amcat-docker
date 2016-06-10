# Amcat version 1.4.1

# VERSION 20160610_1

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

RUN apt-get update && apt-get -y install python-virtualenv python-dev libxml2-dev libxslt-dev python-lxml git 
 
# Create Python VirtualEnv
#RUN virtualenv ~/amcat-env
#RUN /bin/bash ~/amcat-env/bin/activate

# Install python client and scraping framework
RUN pip install git+git://github.com/amcat/amcatclient git+git://github.com/amcat/amcat-scraping

# Copy authentication file for Python client
COPY amcatauth /root/.amcatauth
# Copy scraper settings
COPY scrapers.conf /root/.scrapers.conf

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 
