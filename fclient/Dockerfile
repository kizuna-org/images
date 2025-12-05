FROM golang:1.25@sha256:20b91eda7a9627c127c0225b0d4e8ec927b476fa4130c6760928b849d769c149 AS building

# renovate: datasource=github-releases depName=fatedier/frp
ARG FRP_VERSION=v0.65.0

RUN git clone https://github.com/fatedier/frp.git -b "$FRP_VERSION" /building
WORKDIR /building

RUN make frpc
RUN mv /building/bin/frpc /building/bin/fclient

FROM alpine:3@sha256:4b7ce07002c69e8f3d704a9c5d6fd3053be500b7f1c69fc0d80990c2ad8dd412

RUN apk add --no-cache tzdata

COPY --from=building /building/bin/fclient /usr/bin/fclient

ENTRYPOINT ["/usr/bin/fclient"]
