# nonstop-index
#sudo docker run \
#	-v ~/nsdata:/home/ubuntu/data \
#	-v ~/packages:/home/ubuntu/public \
#	-p 4444:4444 \
#	--name nonstop-index \
#	arob/nonstop-index

FROM nodesource/trusty:0.12.7
MAINTAINER Alex Robson <asrobson@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

USER ubuntu

# install node via NPM and nonstop index
RUN /bin/bash -c "npm install nonstop-index@0.1.10 -g"

# Index HTTP
EXPOSE 4444

# setup directories for data and packages
RUN mkdir /home/ubuntu/data && mkdir /home/ubuntu/public

# expose data and packages as volumes
VOLUME [ "/home/ubuntu/data", "/home/ubuntu/public" ]

CMD /bin/bash -c "nsindex -s"
