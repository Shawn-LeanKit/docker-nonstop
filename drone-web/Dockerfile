# Drone Nonstop Base Build Environment
# This is a (relatively) light-weight baseline Drone build image based on
# nonstop. If you are building Node.js applications with Gulp, it should
# have everything required to produce builds.

FROM markadams/chromium-xvfb
MAINTAINER Alex Robson <asrobson@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# get prerequisities for building native extensions
RUN apt-get update && apt-get -y install curl wget git python build-essential lsb-release

# get drone package
RUN wget http://downloads.drone.io/master/drone.deb && dpkg -i drone.deb
RUN mkdir /etc/drone.d
ADD node.sh /etc/drone.d/node.sh

# install nonstop CLI && gulp
RUN /bin/bash -c "npm install nonstop-cli@0.1.7 -g && npm install gulp -g"
