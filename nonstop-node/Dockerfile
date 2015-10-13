# Nonstop Service Host - Node
# This container runs the Nonstop service host for Node.JS packages.

FROM nodesource/trusty:0.12.7
MAINTAINER Alex Robson <asrobson@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# install node via NPM and nonstop CLI
RUN /bin/bash -c "npm install nonstop@0.1.9 -g"

CMD /bin/bash -c "nonstop"
