FROM getterminus/ruby-docker-images:2.7-je-20210920

RUN echo "deb http://deb.debian.org/debian oldstable main" >> /etc/apt/sources.list

RUN apt-get -y update && apt-get install -y --no-install-recommends \
     apt-utils ca-certificates dnsutils zip nodejs jq \
    libxml2-dev libxslt1-dev libv8-dev npm mc build-essential \
    patch ruby-dev zlib1g-dev liblzma-dev pkg-config libjemalloc-dev \
    gifsicle  mercurial

WORKDIR /tmp

RUN mkdir -p /tmp/vendor/cache
RUN gem install bundler:1.17.3
RUN gem install libv8 -v '3.16.14.19' -- --with-system-v8

RUN hg clone https://hg.osdn.net/view/graphicsmagick/GM GM
WORKDIR /tmp/GM
RUN ./configure  '--build' 'x86_64-linux-gnu' '--enable-shared' '--enable-static' '--enable-libtool-verbose' '--prefix=/usr' \
                '--mandir=${prefix}/share/man' '--infodir=${prefix}/share/info' '--docdir=${prefix}/share/doc/graphicsmagick' \
                '--with-gs-font-dir=/usr/share/fonts/type1/gsfonts' '--with-x' '--x-includes=/usr/include/X11' '--x-libraries=/usr/lib/X11' \
                '--without-dps' '--without-modules' '--without-frozenpaths' '--with-webp=yes' '--with-zstd=yes' '--with-perl' \
                '--with-perl-options=INSTALLDIRS=vendor' '--enable-quantum-library-names' '--with-quantum-depth=16' 'build_alias=x86_64-linux-gnu' \
                'CFLAGS=-g -O2 -fdebug-prefix-map=/build/graphicsmagick-FG5eMj/graphicsmagick-1.4+really1.3.35=. -fstack-protector-strong -Wformat -Werror=format-security' \
                'LDFLAGS=-Wl,-z,relro -Wl,-z,now' 'CPPFLAGS=-Wdate-time -D_FORTIFY_SOURCE=2' 'CXXFLAGS=-g -O2 -fstack-protector-strong -Wformat -Werror=format-security'
RUN make && make install

RUN npm install --global yarn
RUN npm install --global uglify-js@3.15.2
RUN npm install --save uglify-js@github:mishoo/UglifyJS2#harmony
