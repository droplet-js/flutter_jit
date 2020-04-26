# --- build ---

FROM v7lin/depot_tools as build

ENV ENGINE_PATH $HOME/engine

COPY engine $ENGINE_PATH

RUN echo $PWD
RUN ls engine -a

WORKDIR $ENGINE_PATH
RUN gclient sync --verbose

WORKDIR $ENGINE_PATH/src/
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

#ENV PATH=$PATH:/opt/flutter/bin

COPY --from=build /engine /opt/engine