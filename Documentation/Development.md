# Development Environment Setup

## Prerequisites

- [Git](https://git-scm.com/) / [Git Bash](https://gitforwindows.org/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [OpenSSH](https://www.openssh.com/) (Windows)

### Local

- [Node.js LTS v20](https://nodejs.org/en/)
- [Docker + Docker Compose](https://docs.docker.com/desktop/)

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

4. Create a file called .env. Copy and paste the content of .example.env to .env. Also create a github clientId and secretId in Github and add those to the .env file.

## Running Locally

1. Open a new terminal in VSCode (Ctrl + Shift + `)

1. Open the Docker Desktop Client.

1. Start the database

   ```bash
    docker compose -f docker-compose.dev.yaml up --build db
   ```

1. Open a new terminal in VSCode (Ctrl + Shift + `)

1. Install dependencies

    ```bash
    npm install -D
    ```

1. Initialize Prisma

    ```bash
    npm run prisma-init
    ```

1. Run the project

    ```bash
    npm run dev
    ```

1. Test the project

    ```bash
    npm run test
    ```

1. Test the project with coverage

    ```bash
    npm run coverage
    ```

## Running with Docker

1. Open a new terminal in VSCode (Ctrl + Shift + `)

1. Run the project with docker compose

    ```bash
    docker compose -f docker-compose.dev.yaml up --build
    ```

## Linting

1. Open a new terminal in VSCode (Ctrl + Shift + `)

1. Run the project with ESLint

   ```bash
   npm run lint 
   npm run format
   ```

## OpenSSH (For Windows Users Only)

1. Install OpenSSH in Powershell using the following command

   ```bash
   Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
   ```

## Viewing the website

Open <http://localhost:3000> in your browser to view the project

## Setting up OAuth

Create a new new project at <https://console.cloud.google.com>
Setup the OAuth Consent Screen
Go to the Credentials page
Click `+Create Credentials / OAuth Client ID`
Application type web
Set the Authorized redirect URI to <http://localhost:3000/auth/login/google/callback>
Replace the github values in your .env with your new id and secret like so:

```bash
GOOGLE_CLIENT_ID="value_of_google_client_id"
GOOGLE_CLIENT_SECRET="value_of_google_client_secret"
```

With the database running, run the following command

```bash
npx prisma migrate reset
```

If this doesn't work try rebuilding the database.
