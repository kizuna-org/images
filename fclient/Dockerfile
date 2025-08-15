FROM golang:1.25@sha256:9e56f0d0f043a68bb8c47c819e47dc29f6e8f5129b8885bed9d43f058f7f3ed6 AS building

# renovate: datasource=github-releases depName=fatedier/frp
ARG FRP_VERSION=v0.63.0

RUN git clone https://github.com/fatedier/frp.git -b "$FRP_VERSION" /building
WORKDIR /building

RUN make frpc
RUN mv /building/bin/frpc /building/bin/fclient

FROM alpine:3

RUN apk add --no-cache tzdata

COPY --from=building /building/bin/fclient /usr/bin/fclient

ENTRYPOINT ["/usr/bin/fclient"]
