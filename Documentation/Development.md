# Development Environment Setup

## Prerequisites

- [Git](https://git-scm.com/) / [Git Bash](https://gitforwindows.org/)
- [Visual Studio Code](https://code.visualstudio.com/)

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

2. Open the Docker Desktop Client. 

3.  Start the data base
   
   ```bash
    docker compose -f docker-compose.dev.yaml up --build db
   ```

3.   Open a new terminal in VSCode (Ctrl + Shift + `)

4. Install dependencies
    
    ```bash
    npm install -D
    ```
    
5. Initialize Prisma

    ```bash
    npm run prisma-init
    ```

6. Run the project

    ```bash
    npm run dev
    ```

7. Test the project

    ```bash
    npm run test
    ```

8. Test the project with coverage

    ```bash
    npm run coverage
    ```

## Running with Docker

1. Open a new terminal in VSCode (Ctrl + Shift + `)

2. Run the project with docker compose

    ```bash
    docker compose -f docker-compose.dev.yaml up --build
    ```

## Linting

1. Open a new terminal in VSCode (Ctrl + Shift + `)

2. Run the project with ESLint

   ```bash
   npm run lint 
   npm run format
   ```

## Connect to AWS (Mac & Linux)

1. Open a new terminal

2. Verify they key pair with chmod 400

   ```bash
   chmod 400 fmfsam.pem
   ```

3. Connect to the AWS instance using ssh

   ```bash
   ssh -i fmfsam.pem ec2-user@18.222.184.241
   ```

4. To disconnect, type exit

   ```bash
   exit
   ```

## Viewing the website

Open http://localhost:5000 in your browser to view the project
