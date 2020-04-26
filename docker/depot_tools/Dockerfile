FROM ubuntu:16.04

ENV DEPOT_TOOLS_PATH $HOME/depot_tools
ENV PATH $PATH:$DEPOT_TOOLS_PATH

RUN apt-get update && \
    apt-get install -y git wget curl unzip python lsb-release sudo apt-transport-https && \
    git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git $DEPOT_TOOLS_PATH && \
    apt-get clean
