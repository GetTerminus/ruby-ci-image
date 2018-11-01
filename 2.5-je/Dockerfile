FROM getterminus/ruby-docker-images:2.5-je-20181031


RUN apt-get update && apt-get install -y --no-install-recommends \
                unzip \
                apt-transport-https \
                ca-certificates \
                curl \
                gnupg2 \
                software-properties-common \
                && rm -rf /var/lib/apt/lists/*

# install docker
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable"

 RUN apt-get update && apt-get install -y --no-install-recommends \
       docker-ce

RUN curl -L https://convox.com/cli/linux/convox -o /usr/local/bin/convox && chmod 755 /usr/local/bin/convox
