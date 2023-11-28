# Development Environment Setup

## Prerequisites

- [Git](https://git-scm.com/) / [Git Bash](https://gitforwindows.org/)
- [Visual Studio Code](https://code.visualstudio.com/)

### Local

- [Node.js LTS v20](https://nodejs.org/en/)

### Docker

- [Docker + Docker Compose](https://docs.docker.com/desktop/)

## Setup

1. Clone the repository

    ```bash
    git clone https://github.com/Free-My-Financials/free-my-financials.git
    ```

2. Open the repository in VSCode

    ```bash
    code free-my-financials
    ```

3. Accept all recommended extensions from the popup on the bottom right

## Running Locally

1. Open a new terminal in VSCode (Ctrl + Shift + `)

2. Move in to the web directory

    ```bash
    cd web
    ```

3. Install dependencies

    ```bash
    npm install -D
    ```

4. Run the project

    ```bash
    npm run dev
    ```

## Running with Docker

1. Open a new terminal in VSCode (Ctrl + Shift + `)

2. Run the project with docker compose

    ```bash
    docker compose -f docker-compose.dev.yaml up --build
    ```

## Viewing the website

Open http://localhost:3000 in your browser to view the project
