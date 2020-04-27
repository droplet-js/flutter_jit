FROM alpine:3.9 as download

ENV FLUTTER_CHANNEL=stable
ENV FLUTTER_VERSION=1.12.13+hotfix.9

RUN wget --output-document=flutter.tar.xz https://storage.googleapis.com/flutter_infra/releases/${FLUTTER_CHANNEL}/linux/flutter_linux_v${FLUTTER_VERSION}-${FLUTTER_CHANNEL}.tar.xz \
    && tar xf flutter.tar.xz -C /opt

# --- build ---

FROM v7lin/depot_tools as build

ENV ENGINE_GITURL=https://github.com/flutter/engine.git
ENV ENGINE_PATH=$HOME/engine

COPY engine $ENGINE_PATH
COPY --from=download /opt/flutter/bin/internal/engine.version $ENGINE_PATH

WORKDIR $ENGINE_PATH
RUN ENGINE_VERSION=$(cat engine.version) && sed -i "s|$ENGINE_GITURL|$ENGINE_GITURL@$ENGINE_VERSION|g" .gclient
RUN gclient sync --verbose

WORKDIR $ENGINE_PATH/src
# arm
RUN ./flutter/tools/gn --android --runtime-mode jit_release --android-cpu arm && \
    ninja -C out/android_jit_release
RUN ./flutter/tools/gn --runtime-mode jit_release --android-cpu arm && \
    ninja -C out/host_jit_release
# arm64
RUN ./flutter/tools/gn --android --runtime-mode jit_release --android-cpu arm64 && \
    ninja -C out/android_jit_release_arm64
RUN ./flutter/tools/gn --runtime-mode jit_release --android-cpu arm64 && \
    ninja -C out/host_jit_release_arm64

# --- prod ---

FROM runmymind/docker-android-sdk as prod

MAINTAINER v7lin <v7lin@qq.com>

ENV PATH=$PATH:/opt/flutter/bin
ENV ENGINE_PATH=/opt/engine

COPY --from=download /opt/flutter /opt/flutter
COPY --from=build /engine /opt/engine
