# Go VSCode DevContainer

A sandbox for Go programming language by using vscode devcontainer.

## Getting Started

- Setup `docker` and `docker compose` on your local machine
- Set dev/.gitconfig & env 
- `docker compose up -d dev`

## .gitconfig

```txt
[credential]
    helper = store
[credential "https://github.com"]
    username = xxxx
    password = xxxx
```

## Environment

See docker-compose.yml

- CONTAINER_PORT