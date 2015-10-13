# Nonstop Service Host - CoffeeScript
# This container runs the Nonstop service host for CoffeeScript packages (i.e. hubot).

FROM arob/nonstop-node:0.12.7-0.1.9
MAINTAINER Alex Robson <asrobson@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# install node via NPM and nonstop CLI
RUN /bin/bash -c "npm install coffee-script -g"

CMD /bin/bash -c "nonstop"
