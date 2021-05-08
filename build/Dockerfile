FROM ubuntu:16.04

RUN apt update \
    && apt install -y socat libc6-armel-cross libpixman-1-dev libfdt-dev wget patch \
    && apt install -y build-essential zlib1g-dev pkg-config libglib2.0-dev binutils-dev libboost-all-dev autoconf libtool libssl-dev libpixman-1-dev libpython-dev python-pip python-capstone virtualenv

COPY ./qemu-2.7.0.tar.gz ./
RUN tar xzf qemu-2.7.0.tar.gz \
    && mv qemu-2.7.0 qemu-2.7.0.orig
COPY qemu-2.7.0-aslr_nx_wxorx.patch .
RUN patch -s -p0 < qemu-2.7.0-aslr_nx_wxorx.patch
RUN mkdir /root/qemu-patch
RUN mv qemu-2.7.0.orig qemu-2.7.0 \
    && cd qemu-2.7.0 \
    && ./configure --prefix=/root/qemu-patch --target-list=cris-linux-user,mipsn32-linux-user,unicore32-linux-user,mipsn32el-linux-user,x86_64-linux-user,ppc64le-linux-user,mipsel-linux-user,mips64-linux-user,sh4eb-linux-user,mips-linux-user,m68k-linux-user,aarch64-linux-user,sparc-linux-user,ppc64abi32-linux-user,s390x-linux-user,sh4-linux-user,tilegx-linux-user,alpha-linux-user,microblazeel-linux-user,sparc64-linux-user,arm-linux-user,sparc32plus-linux-user,armeb-linux-user,mips64el-linux-user,i386-linux-user,ppc-linux-user,microblaze-linux-user,or32-linux-user,ppc64-linux-user --disable-werror --static \
    && make all
RUN cd /qemu-2.7.0 && make install
