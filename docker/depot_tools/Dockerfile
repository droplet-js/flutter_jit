FROM ubuntu:16.04

ENV DEPOT_TOOLS_PATH $HOME/depot_tools
ENV PATH $PATH:$DEPOT_TOOLS_PATH

RUN apt-get update && \
    apt-get install -y git wget curl unzip python lsb-release sudo apt-transport-https && \
    git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git $DEPOT_TOOLS_PATH && \
    mkdir --parents $ENGINE_PATH && \
    git clone https://github.com/flutter/buildroot.git $BUILDROOT_PATH && \
    cd $BUILDROOT_PATH && \
    ./build/install-build-deps.sh --no-prompt && \
    ./build/install-build-deps-android.sh --no-prompt && \
    apt-get clean
