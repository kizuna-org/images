FROM golang:1.23@sha256:8b9a1e34c73ab8a774613c6b66cd92c750d1eeaa72c914b551026156ca5a8c52 AS building

# renovate: datasource=github-releases depName=fatedier/frp
ARG FRP_VERSION=v0.63.0

RUN git clone https://github.com/fatedier/frp.git -b "$FRP_VERSION" /building
WORKDIR /building

RUN make frpc
RUN mv /building/bin/frpc /building/bin/fclient

FROM alpine:3@sha256:4bcff63911fcb4448bd4fdacec207030997caf25e9bea4045fa6c8c44de311d1

RUN apk add --no-cache tzdata

COPY --from=building /building/bin/fclient /usr/bin/fclient

ENTRYPOINT ["/usr/bin/fclient"]
