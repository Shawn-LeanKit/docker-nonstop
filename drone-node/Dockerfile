# Drone Nonstop Base Build Environment
# This is a (relatively) light-weight baseline Drone build image based on
# nonstop. If you are building Node.js applications with Gulp, it should
# have everything required to produce builds.

FROM nodesource/trusty:0.12.7
MAINTAINER Alex Robson <asrobson@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# get drone package
# ADD drone.deb drone.deb
USER root
ADD node.sh /home/ubuntu/node.sh
RUN apt-get -y install wget
RUN wget http://downloads.drone.io/master/drone.deb
RUN dpkg -i drone.deb
RUN mkdir /etc/drone.d && cp /home/ubuntu/node.sh /etc/drone.d/node.sh

USER ubuntu

# install nonstop CLI and gulp
RUN /bin/bash -c "npm install nonstop-cli@0.1.7 -g && npm install gulp -g"
