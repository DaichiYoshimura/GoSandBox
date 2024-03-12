FROM golang:1.22.1-alpine3.19

ARG GITCONFIG_EMAIL
ARG GITCONFIG_NAME
ARG REPO_URL

# Install necessary packages
RUN apk update && \
    apk add --no-cache tzdata git git-prompt git-zsh-completion zsh ca-certificates vim curl make && \
    update-ca-certificates

# Set timezone to Asia/Tokyo
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# Configure Git and Zsh
RUN git config --global user.email "${GITCONFIG_EMAIL}" && \
    git config --global user.name "${GITCONFIG_NAME}" && \
    sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

# Clone repository
RUN mkdir -p /go/src/app && \
    git clone ${REPO_URL} /go/src/app

# Set working directory
WORKDIR /go/src/app

# Install Go tools
RUN go install golang.org/x/tools/gopls@latest
RUN go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest
RUN go install github.com/go-delve/delve/cmd/dlv@latest
RUN go install github.com/cosmtrek/air@latest
RUN go install github.com/google/wire/cmd/wire@latest

# Set environment variables
ENV GOPATH=/go \
    PATH=$PATH:/go/bin

# Set default entrypoint
ENTRYPOINT ["/bin/zsh"]
