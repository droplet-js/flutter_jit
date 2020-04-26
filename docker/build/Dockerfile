# --- build ---

FROM v7lin/depot_tools as build

COPY engine engine

RUN ls engine

# --- prod ---

FROM alpine:3.9 as prod