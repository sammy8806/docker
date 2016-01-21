FROM ubuntu:xenial
MAINTAINER sammy8806

RUN apt-get update; apt-get upgrade -y
RUN apt-get install -y build-essential
RUN apt-get install -y git subversion wget curl grep gawk
RUN apt-get install -y ca-certificates

# Dependencies
RUN apt-get install -y openssl
RUN mkdir /nodejs && wget -q "https://nodejs.org/dist/v5.4.1/node-v5.4.3-linux-x64.tar.gz" | tar xvzf - -C /nodejs --strip-components=1
RUN ln -s /nodejs/bin/node /usr/bin/node
RUN ln -s /nodejs/bin/npm /usr/bin/npm
RUN echo "export PATH=\"/nodejs/bin:$PATH\"""
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
    echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list && \
    apt-get update && \
    apt-get install -y pwgen mongodb-org mongodb-org-server mongodb-org-shell mongodb-org-mongos mongodb-org-tools && \
    echo "mongodb-org hold" | dpkg --set-selections && \
    echo "mongodb-org-server hold" | dpkg --set-selections && \
    echo "mongodb-org-shell hold" | dpkg --set-selections && \
    echo "mongodb-org-mongos hold" | dpkg --set-selections && \
    echo "mongodb-org-tools hold" | dpkg --set-selections

# colorize output of make
RUN apt-get install -y colormake
RUN echo "alias make='colormake '\n" >> /etc/bash.bashrc

ENV PATH $PATH:/nodejs/bin
CMD ["/bin/bash"]
