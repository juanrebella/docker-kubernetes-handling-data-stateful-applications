FROM golang:1.15.14-alpine3.14 AS builder
ENV CGO_ENABLED=0

WORKDIR /go/stock-api
COPY ./src/go.mod .
RUN go mod download 

COPY ./src .
RUN go build -o /server

# app
FROM alpine:3.14

ENV POSTGRES_CONNECTION_STRING="host=products-db port=5432 user=postgres password=wired dbname=postgres sslmode=disable" \
    CACHE_EXPIRY_SECONDS="45"

EXPOSE 8080
CMD ["/app/server"]

WORKDIR /cache
WORKDIR /app
COPY --from=builder /server .