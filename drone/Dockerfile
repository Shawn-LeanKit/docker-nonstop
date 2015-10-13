# Docker image for the Drone CI system.
# Be sure to create a local drone.toml from the included example
# and set your source control credentials there before building.
# To use my image the following command will start the container:
#    docker run --privileged \
#				--name drone \
#				-p [host]:80
#				-v [hostpath]:/var/lib/docker
#				-v [hostpath]:/var/lib/drone
#				-e DRONE_GITHUB_CLIENT="[your client application id]"
#				-e DRONE_GITHUB_SECRET="[your client application secret]"
#				arob/drone
FROM ubuntu:14.04

MAINTAINER Alex Robson <alex.robson@leankit.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y curl
RUN curl -s https://get.docker.io/ubuntu/ | sh
RUN echo 'DOCKER_OPTS="-H :2375 -H unix:///var/run/docker.sock"' >> /etc/default/docker
RUN apt-get -y install htop

# Install drone from the latest release
RUN apt-get -y install wget
RUN wget http://downloads.drone.io/master/drone.deb
RUN dpkg -i drone.deb

# Docker daemon
EXPOSE 2375

# Drone HTTP
EXPOSE 80

# Add drone configuration
ADD drone.toml /etc/drone/drone.toml

CMD /etc/init.d/docker start && /usr/local/bin/droned --config=/etc/drone/drone.toml
