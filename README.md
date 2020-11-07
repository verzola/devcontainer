# devcontainer-base
Development container with common tools for web development with JavaScript and PHP.

## Requirements
- [Docker](https://docs.docker.com/get-docker/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Remote Containers extension](https://code.visualstudio.com/docs/remote/containers)

## Setup
1. Copy the `.devcontainer` folder to your project;
2. Open the project with VSCode;
3. Click on "Reopen in Container" when it pop ups on the bottom right;
![Reopen in container](img/popup.png)
4. Wait a minute;
5. Done!

## Comes with
- Zsh
- Oh My Zsh
- Fzf
- Docker
- Docker Compose
- PHP
- Composer
- NodeJS
- NPM
- Yarn

## Extensions
General extensions are installed by default, but specific extensions are commented and separated by language.
To choose what extensions should be installed inside the container, uncomment the sections in `.devcontainer/devcontainer.json`.