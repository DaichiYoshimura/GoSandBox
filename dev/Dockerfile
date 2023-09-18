FROM golang:1.21.1-alpine3.18

ARG GITCONFIG_EMAIL
ARG GITCONFIG_NAME
ARG USER_NAME
ARG APP_NAME
ARG UID
ARG GID

# vscode *******************************************
RUN addgroup -S ${GID} && \
    adduser -S ${UID} -G ${GID}
USER ${USER}
# **************************************************

RUN apk update

# time *********************************************
RUN apk add tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
# **************************************************

# git **********************************************
RUN apk add git git-prompt git-zsh-completion && \
    git config --global user.email ${GITCONFIG_EMAIL} && \
    git config --global user.name ${GITCONFIG_NAME}
# **************************************************

# zsh **********************************************
RUN apk add zsh && \
    sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
ENTRYPOINT /bin/zsh
# **************************************************

# https ********************************************
RUN apk add --no-cache ca-certificates && update-ca-certificates
ENV SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
ENV SSL_CERT_DIR=/etc/ssl/certs
# **************************************************

# the others ...
RUN apk add vim curl make

# go ************************************************
RUN go install golang.org/x/tools/gopls@latest && \
    go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest && \
    go install github.com/go-delve/delve/cmd/dlv@latest && \
    go install github.com/cosmtrek/air@latest
# ***************************************************

RUN mkdir /go/src/${APP_NAME}
WORKDIR /go/src/${APP_NAME}