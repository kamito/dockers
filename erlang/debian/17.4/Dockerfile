FROM debian
MAINTAINER s-kamito@groovenauts.jp

# dependency packages
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y \
    build-essential make autoconf automake gcc g++ tcl8.5 systemtap systemtap-sdt-dev \
    libncurses5-dev openssl libssl-dev curl git-core \
    dh-make devscripts debhelper fakeroot lintian sudo pbuilder piuparts dpatch quilt

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
