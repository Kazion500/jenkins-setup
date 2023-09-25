FROM golang:1.21 as builder

WORKDIR /usr/src/app

# pre-copy/cache go.mod for pre-downloading dependencies and only redownloading them in subsequent builds if they change
COPY go.mod go.sum ./
RUN go mod download && go mod verify

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -v -o /usr/local/bin/app


FROM gcr.io/distroless/base-debian11 AS build-release-stage

WORKDIR /

COPY --from=builder /usr/local/bin/app /usr/local/bin/app

EXPOSE 3000

USER nonroot:nonroot

CMD ["app"]