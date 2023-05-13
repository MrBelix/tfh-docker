ARG NODE_VERSION=12

FROM ubuntu:22.04

RUN apt update && apt install -y python2 python3 curl \
	&& curl -sL https://deb.nodesource.com/setup_18.x -o nodesource_setup.sh \
	&& apt -y install nodejs npm

WORKDIR /app