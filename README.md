# Go VSCode DevContainer

A sandbox for Go programming language by using vscode devcontainer.

## Getting Started

- Setup `docker` and `docker compose` on your local machine
- `npm install -g @devcontainers/cli`
- `docker compose up -d dev`
- `devcontainer open dev` <- deprecated! use gui.

## Set up `.env`

To set up git config, add `.env` file and write env vars.  

```.env
GITCONFIG_EMAIL=your@email.address
GITCONFIG_NAME=yourname
APP_NAME=awsomeapp
```
