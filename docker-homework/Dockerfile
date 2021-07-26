# stage 1
FROM golang:alpine as golangapp

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN go build -o api

# Stage 2
FROM alpine:latest

COPY --from=golangapp /app/api .
COPY config/app/.env .
COPY config/app/app.conf .

CMD ./api