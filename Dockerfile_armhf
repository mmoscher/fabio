FROM arm32v7/golang:1.13.5 AS build

ARG consul_version=1.6.1
ADD https://releases.hashicorp.com/consul/${consul_version}/consul_${consul_version}_linux_armhfv6.zip /usr/local/bin
RUN cd /usr/local/bin && unzip consul_${consul_version}_linux_armhfv6.zip

ARG vault_version=1.2.3
ADD https://releases.hashicorp.com/vault/${vault_version}/vault_${vault_version}_linux_arm.zip /usr/local/bin
RUN cd /usr/local/bin && unzip vault_${vault_version}_linux_arm.zip

WORKDIR /src
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 go test -mod=vendor -trimpath -ldflags "-s -w" ./...
RUN CGO_ENABLED=0 GOOS=linux GOARCH=arm GOARM=7 go build -mod=vendor -trimpath -ldflags "-s -w"

FROM arm32v7/alpine:3.10
RUN apk update && apk add --no-cache ca-certificates
COPY --from=build /src/fabio /usr/bin
ADD fabio.properties /etc/fabio/fabio.properties
EXPOSE 9998 9999
ENTRYPOINT ["/usr/bin/fabio"]
CMD ["-cfg", "/etc/fabio/fabio.properties"]
