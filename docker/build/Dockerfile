# --- build ---

FROM v7lin/depot_tools as build

ENV ENGINE_PATH $HOME/engine

COPY engine $ENGINE_PATH

RUN ls engine -a

# --- prod ---

FROM alpine:3.9 as prod