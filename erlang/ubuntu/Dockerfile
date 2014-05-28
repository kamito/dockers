# from ubuntu image
# via https://index.docker.io/_/ubuntu/
FROM ubuntu

RUN apt-get -y update
RUN apt-get -y install curl wget autoconf automake autotools-dev \
    libtool pkg-config zlib1g-dev libcunit1-dev libssl-dev libxml2-dev libevent-dev \
    build-essential libncurses5-dev openssl libssl-dev curl git-core vim dstat \
    systemtap systemtap-sdt-dev

RUN curl -OL http://www.erlang.org/download/otp_src_R16B03-1.tar.gz && \
    tar xzf otp_src_R16B03-1.tar.gz && \
    cd otp_src_R16B03-1 && \
    ./configure --prefix=/opt/erlang/R16B03-1 --enable-smp-support --enable-threads \
    --enable-m64-build --enable-vm-probes --enable-kernel-poll --disable-hipe \
    --with-dynamic-trace=systemtap --without-javac --enable-native-libs --disable-sctp && \
    make && \
    make install && \
    echo "\n\nPATH=/opt/erlang/R16B03-1/bin:$PATH" >> /etc/profile
    source /etc/profile
