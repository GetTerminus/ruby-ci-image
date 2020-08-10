FROM getterminus/ruby-docker-images:2.6-je-20190204

RUN apt-get update && apt-get install -y --no-install-recommends \
                unzip \
                apt-transport-https \
                ca-certificates \
                curl \
                gnupg2 \
                software-properties-common \
                make \
                libssl-dev \
                libghc-zlib-dev \
                libcurl4-gnutls-dev \
                libexpat1-dev \
                gettext \
                && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/git/git/archive/v2.18.0.tar.gz -O git.tar.gz
RUN tar -xf git.tar.gz
RUN cd git-*; \
    make prefix=/usr/local all; \
    make prefix=/usr/local install
RUN git version

# install docker
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"

 RUN apt-get update && apt-get install -y --no-install-recommends \
       docker-ce

RUN curl -L https://convox.com/cli/linux/convox -o /usr/local/bin/convox && chmod 755 /usr/local/bin/convox
