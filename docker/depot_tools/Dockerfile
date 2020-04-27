FROM ubuntu:18.04

ENV DEPOT_TOOLS_PATH=$HOME/depot_tools
ENV BUILDROOT_PATH=$HOME/buildroot
ENV PATH=$PATH:$DEPOT_TOOLS_PATH

RUN apt-get update
RUN apt-get install -y git wget curl unzip python lsb-release sudo apt-transport-https
RUN git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git $DEPOT_TOOLS_PATH
RUN git clone https://github.com/flutter/buildroot.git $BUILDROOT_PATH
RUN cd $BUILDROOT_PATH && ./build/install-build-deps.sh --no-prompt && ./build/install-build-deps-android.sh --no-prompt
RUN apt-get clean
