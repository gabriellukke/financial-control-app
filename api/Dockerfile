FROM golang:1.22-alpine AS builder

# Set working directory inside the container
WORKDIR /app

# Copy Go mod and sum files, and download dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest of the application source code
COPY . .

# Build the application binary
RUN go build -o webapi .

# Stage 2: Run the Go application in a lightweight container
FROM alpine:latest

# Set working directory inside the container
WORKDIR /app

# Copy the binary from the builder stage
COPY --from=builder /app/webapi .

# Expose the port on which the app will run
EXPOSE 8080

# Command to run the web API
CMD ["./webapi"]
