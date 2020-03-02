FROM golang as builder

RUN apt-get update && apt-get install -y ca-certificates

RUN git clone -b v1.6.5 --depth=1 https://github.com/drone/drone
RUN cd drone && go build -o /opt/drone-server -tags "oss nolimit" ./cmd/drone-server

FROM debian:buster-slim 

COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /opt/drone-server /

EXPOSE 80 443
VOLUME /data

ENTRYPOINT [ "/drone-server" ]