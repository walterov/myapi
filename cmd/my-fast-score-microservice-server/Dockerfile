FROM golang:1.10.3-alpine3.8

RUN apk add git

COPY . /go/src/github.com/walterov/myapi/cmd/my-fast-score-microservice-server
WORKDIR /go/src/github.com/walterov/myapi/restapi

WORKDIR /go/src/github.com/walterov/myapi/cmd/my-fast-score-microservice-server

RUN go get
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo

FROM scratch

COPY --from=0 /go/src/github.com/walterov/myapi/cmd/my-fast-score-microservice-server/my-fast-score-microservice-server /my-fast-score-microservice-server
COPY keys /keys

ENV PORT 8123
ENV TLS_CERT keys/dummy.crt
ENV TLS_KEY keys/dummy.key
ENV TLS_HOST 0.0.0.0

CMD [ "/my-fast-score-microservice-server" ]

