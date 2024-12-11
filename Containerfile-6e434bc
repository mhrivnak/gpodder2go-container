FROM registry.access.redhat.com/ubi9/go-toolset:latest as builder

RUN mkdir $HOME/build

COPY 6e434bc.zip $HOME/build/

WORKDIR $HOME/build

RUN unzip 6e434bc.zip

WORKDIR gpodder2go-6e434bc63ce45c84b3597d6debeb0156ff8656f6

RUN ls -lh

RUN CGO_ENABLED=0 GOOS=linux go build -o $HOME/gpodder2go

FROM registry.access.redhat.com/ubi9/ubi-micro:latest

RUN mkdir /data && chown -R 1001:0 /data && chmod -R g=u /data

WORKDIR /data

COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /data /entrypoint.sh

COPY --from=builder /opt/app-root/src/gpodder2go /usr/bin/gpodder2go

EXPOSE 3005
USER 1001
VOLUME /data
ENTRYPOINT ["/entrypoint.sh"]
