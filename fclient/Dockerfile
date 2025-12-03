FROM golang:1.25@sha256:e68f6a00e88586577fafa4d9cefad1349c2be70d21244321321c407474ff9bf2 AS building

# renovate: datasource=github-releases depName=fatedier/frp
ARG FRP_VERSION=v0.65.0

RUN git clone https://github.com/fatedier/frp.git -b "$FRP_VERSION" /building
WORKDIR /building

RUN make frpc
RUN mv /building/bin/frpc /building/bin/fclient

FROM alpine:3@sha256:51183f2cfa6320055da30872f211093f9ff1d3cf06f39a0bdb212314c5dc7375

RUN apk add --no-cache tzdata

COPY --from=building /building/bin/fclient /usr/bin/fclient

ENTRYPOINT ["/usr/bin/fclient"]
