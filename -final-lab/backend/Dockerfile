# Stage 1: Build (Ex-3.6 Multi-stage build)
FROM golang:1.21-alpine AS build-stage
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
# Build ra file thực thi tên là "server"
RUN go build -o /server app.go

# Stage 2: Runtime (Ex-3.4, 3.5 Optimize size)
FROM alpine:3.18
WORKDIR /
COPY --from=build-stage /server /server

# Ex-3.3: Tạo user non-root để bảo mật
RUN adduser -D appuser
USER appuser

EXPOSE 8080
CMD ["/server"]