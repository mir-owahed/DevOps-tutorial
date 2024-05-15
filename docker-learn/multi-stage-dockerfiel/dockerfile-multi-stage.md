```
FROM golang:1.22-alpine AS builder

WORKDIR /build

COPY . .

RUN CGO_ENABLED=0 go build -o ./go-lang-app

FROM gcr.io/distroless/base-debian12
WORKDIR /app
COPY --from=builder /build/go-lang-app ./go-lang-app
EXPOSE 8000
CMD ["./go-lang-app"]
```
