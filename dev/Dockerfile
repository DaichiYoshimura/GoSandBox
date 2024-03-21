FROM golang:1.22.1-alpine3.19

# Install necessary packages
RUN apk update && \
    apk add --no-cache openssh-client tzdata git zsh ca-certificates vim curl make wget && \
    update-ca-certificates

# Set timezone to Asia/Tokyo
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# Configure Git and Zsh
RUN sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

# Set working directory
WORKDIR /go/src/app

# Install Go tools
RUN go install golang.org/x/tools/gopls@latest
RUN go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
RUN go install github.com/go-delve/delve/cmd/dlv@latest

# Set environment variables
ENV GOPATH=/go \
    PATH=$PATH:/go/bin

# Set default entrypoint
ENTRYPOINT ["/bin/zsh"]
