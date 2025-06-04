FROM golang:1.23rc1


WORKDIR /go/src/app

COPY . .

RUN go mod init dispatch || true
RUN go mod tidy
RUN go build -o dispatch

CMD ["./dispatch"]
