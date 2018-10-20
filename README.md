# devops
first create one awsec2 instance and then install packeges whenever going to install in the same have to install packesges based server requirement(by using ansible and shellscript
#!/bin/sh
apt-get update  # To get the latest package lists
apt-get install <package name> -y
  and ansible already updated playbook,so by using above playbook we can install packages
  once installation completed in msates server and then set up configuration file(/etc/ansible/ansible.cfg
  and set up the inventoryfile and host file and install the boto library(pip-is the cammand for installing the boto)
  and set up the aws credentials(accesskey and secret key) in ~/.boto(it is python library file).
  crate docker file 
      FROM ubuntu:16.04
      MAINTAINER uma
      RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
      ENV APACHE_RUN_USER www-data
      ENV APACHE_RUN_GROUP www-data
      ENV APACHE_LOG_DIR /var/log/apache2
      EXPOSE 80
      CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
  # docker build -t apacheimg -f ./Dockerfileapache .
  # docker run -d -p 80:80 -v /var/www/html:/var/www/html apacheimg 
setup couchdb in MSR-test-Instance-2
     Dockerfile to build couchDB container images
# Based on Ubuntu
############################################################
# Set the base image to Ubuntu
FROM ubuntu

# File Author / Maintainer
MAINTAINER Example uma

# Update the repository sources list
RUN apt-get update
################## BEGIN INSTALLATION ######################
# Install couchDB Following the Instructions at couchDB Docs
# Ref: http://docs.couchDB.org/manual/tutorial/install-couchDB-on-ubuntu/
# Add the package verification key
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

# Add couchDB to the repository sources list
RUN echo 'deb http://downloads-distro.couchDB.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/couchDB.list

# Update the repository sources list once more
RUN apt-get update

# Install couchDB package (.deb)
RUN apt-get install -y couchDB-10gen

# Create the default data directory
RUN mkdir -p /data/db
##################### INSTALLATION END #####################
# Expose the default port
EXPOSE 27017

# Default port to execute the entrypoint (couchDB)
CMD ["/usr/bin/couchDB", "--config", "/etc/couchDB.conf"]

       
