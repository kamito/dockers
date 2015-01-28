FROM debian
MAINTAINER s-kamito@groovenauts.jp

# dependency packages
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y --no-install-recommends \
    build-essential make autoconf automake gcc g++ tcl8.5 systemtap systemtap-sdt-dev \
    libncurses5-dev openssl libssl-dev curl git-core \
    dh-make devscripts debhelper fakeroot lintian sudo pbuilder piuparts dpatch quilt \
    python-setuptools protobuf-c-compiler

# Protobuffs
RUN apt-get update
RUN apt-get -y install openjdk-7-jdk --no-install-recommends
RUN update-alternatives --set java /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java
RUN apt-get -y install maven --no-install-recommends
RUN cd /tmp\
    && wget http://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz \
    && tar zxvf protobuf-2.5.0.tar.gz \
    && cd protobuf-2.5.0 \
    && ./configure --prefix=/usr \
    && make \
    && make install

# Erlang install
RUN mkdir /tmp/erlang
RUN cd /tmp/erlang \
    && curl -O http://www.erlang.org/download/otp_src_17.4.tar.gz \
    && tar zxvf otp_src_17.4.tar.gz \
    && cd otp_src_17.4/ \
    && ./configure --enable-m64-build --enable-smp-support --enable-threads \
                   --enable-vm-probes --enable-kernel-poll --with-dynamic-trace=systemtap \
                   --enable-sctp --enable-hipe --without-javac \
    && make \
    && make install

CMD ["erl"]
