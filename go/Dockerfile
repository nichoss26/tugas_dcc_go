# Stage 1: Base image with Go
FROM golang:1.20-alpine as base

# Stage 2: Build the app
FROM base as builder
WORKDIR /app

# Copy all source files
COPY . .

# Build the Go binary
RUN mkdir -p /app/bin && go build -o /app/bin/app /app/main.go

# Stage 3: Minimal runtime image
FROM gcr.io/distroless/static-debian12

# Copy binary from builder
COPY --from=builder /app/bin/app /app/bin/

# Expose port if needed
EXPOSE 8080

# Run the app
ENTRYPOINT ["/app/bin/app"]
