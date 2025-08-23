FROM golang:1.25@sha256:4859242e2c392ddc9d3225fd41181c00a443d9cc005b8e5131ce164106fbc676 AS building

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
