# syntax=docker/dockerfile:1

FROM golang:1.17-bullseye AS builder
WORKDIR /src

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 \
    go build -ldflags="-s -w" -o /out/momo-store ./cmd/api

FROM debian:bullseye-slim

RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -r -u 10001 -g users appuser
USER 10001

WORKDIR /app
COPY --from=builder /out/momo-store /usr/local/bin/momo-store

EXPOSE 8081
ENV TZ=UTC
CMD ["momo-store"]
