FROM debian
MAINTAINER s-kamito@groovenauts.jp

# use Japan mirror
RUN sed -i -e s@http://http.debian.net/debian@http://ftp.jp.debian.org/debian@ /etc/apt/sources.list

# dependency packages
RUN apt-get update \
    && apt-get upgrade -y\
    && apt-get install -y --no-install-recommends \
      build-essential make autoconf automake gcc g++ tcl8.5 systemtap systemtap-sdt-dev \
      libncurses5-dev openssl libssl-dev curl git-core \
      dh-make devscripts debhelper fakeroot lintian sudo pbuilder piuparts dpatch quilt \
      python-setuptools protobuf-c-compiler \
    && apt-get clean

# Protobuffs
RUN apt-get -y install openjdk-7-jdk --no-install-recommends \
    && update-alternatives --set java /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java \
    && apt-get -y install maven --no-install-recommends \
    && apt-get clean
RUN cd /tmp\
    && wget http://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz \
    && tar xf protobuf-2.5.0.tar.gz \
    && cd protobuf-2.5.0 \
    && ./configure --prefix=/usr \
    && make -j `nproc` \
    && make install \
    && cd / \
    && rm -rf /tmp/protobuf-2.5.0.tar.gz /tmp/protobuf-2.5.0

# Erlang install
RUN mkdir /tmp/erlang \
    && cd /tmp/erlang \
    && curl -O http://download.basho.co.jp.cs-ap-e2.ycloud.jp/otp/download/otp_src_17.4.tar.gz \
    && tar xf otp_src_17.4.tar.gz \
    && cd otp_src_17.4/ \
    && ./configure --enable-m64-build --enable-smp-support --enable-threads \
                   --enable-vm-probes --enable-kernel-poll --with-dynamic-trace=systemtap \
                   --enable-sctp --enable-hipe --without-javac \
    && make -j `nproc` \
    && make install \
    && cd / \
    && rm -rf /tmp/erlang

CMD ["erl"]
