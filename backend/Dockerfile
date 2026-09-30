# ---------- Build stage ----------
FROM golang:1.24 AS builder

WORKDIR /app

# Copy dependency files first
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy application source
COPY . .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -o shopverse-backend ./cmd

# ---------- Runtime stage ----------
FROM alpine:3.20

WORKDIR /app

# Install CA certificates
RUN apk add --no-cache ca-certificates

# Copy compiled application
COPY --from=builder /app/shopverse-backend .

# Application port
EXPOSE 5000

# Start application
CMD ["./shopverse-backend"]
