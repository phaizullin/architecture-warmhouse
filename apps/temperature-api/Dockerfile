FROM golang:1.19-alpine AS builder

WORKDIR /app

COPY . .

RUN go mod init temperature-api && \
    go mod tidy && \
    go build -o temperature-api .

FROM alpine:3.17

WORKDIR /app

COPY --from=builder /app/temperature-api .

EXPOSE 8081

HEALTHCHECK --interval=5s --timeout=3s --start-period=5s --retries=3 \
  CMD wget -q -O- http://localhost:8081/health || exit 1

CMD ["./temperature-api"] 