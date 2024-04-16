# Deployment on AWS

Free My Financials is deployed on AWS using Amplify and EC2. The following steps
should get you started!

## Setting up AWS Amplify

1. Create a new app on [AWS
   Amplify](https://console.aws.amazon.com/amplify/home) by clicking `New app /
   Host web app`
1. Select GitHub and click continue
1. Select the `Free-My-Financials/free-my-financials` repository
1. Select the `main` branch and click next
1. Edit the build settings, replacing them with the following

    ```yaml
    version: 1
    frontend:
        phases:
            preBuild:
                commands:
                    - corepack enable
                    - npx --yes nypm i
                    - npx prisma migrate deploy
            build:
                commands:
                    - env | grep -e DATABASE_URL -e BASE_URL >> .env
                    - env | grep -e GOOGLE_CLIENT_ID -e GOOGLE_CLIENT_SECRET >> .env
                    - npm run build
        artifacts:
            baseDirectory: .amplify-hosting
            files:
                - '**/*'
    ```

1. Check `Enable SSR app logs (optional)` for easier debugging should issues arise
1. Click next
1. Verify all information is correct, then click `Save and deploy`
1. Note down the URL of the deployed app for later

## Setting up AWS EC2 for the Database

1. Create a new EC2 instance on [AWS](https://console.aws.amazon.com/ec2/v2/home) by clicking `Launch instances`
1. Select the `Ubuntu`
1. Create a new key pair and download it
1. Launch the instance
1. Note down the public IP address of the instance for later
1. Click the `Connect` button, and the click the new `Connect` button at the bottom of the page
1. Run the following commands to install the necessary software

    ```bash
    sudo apt update
    sudo apt install postgresql postgresql-contrib
    ```

1. Run the following commands to configure the database, replacing `myPassword` with your desired database password

    ```bash
    sudo -u postgres psql
    ```

    ```sql
    ALTER USER postgres PASSWORD 'myPassword';
    \q
    ```

1. Run the following commands to configure the database to allow connections from any IP address

    ```bash
    sudo nano /etc/postgresql/14/main/pg_hba.conf
    ```

    Add the following line to the bottom of the file

    ```conf
    host    all          all            0.0.0.0/0  md5
    ```

    Save and exit the file. Then run

    ```bash
    sudo nano /etc/postgresql/14/main/postgresql.conf
    ```

    Find the line that says `#listen_addresses = 'localhost'` and change it to `listen_addresses = '*'`

    Save and exit the file.

1. Restart the database

    ```bash
    sudo systemctl restart postgresql
    ```
1. Exit the shell and return to the EC2 dashboard
1. Click the `Security groups` link on the left side
1. Click the security group associated with the EC2 instance (it should be named something like `launch-wizard-1`)
1. Click the `Inbound rules` tab
1. Click `Edit inbound rules`
1. Add a new rule with the following settings

    ```conf
    Type: PostgreSQL
    Protocol: TCP
    Port range: 5432
    Source: Anywhere-IPv4
    ```

## Setting up Google OAuth

1. Create a new new project at <https://console.cloud.google.com>
1. Click `APIs & Services`
1. Setup the OAuth Consent Screen
    1. Make sure to set to `In Production` so that the app can be used by others
1. Go to the Credentials page
1. Click `+Create Credentials / OAuth Client ID`
1. Select application type web
1. Set the Authorized redirect URI to the URL of the deployed app followed by `/auth/login/google/callback`, e.g. `https://main.d1p7xd1nxyc6rx.amplifyapp.com/auth/login/google/callback`
1. Click create
1. Note down the client ID and client secret for later

## Setting up deployment

1. From the AWS Amplify console, click the app you created earlier
1. Click `Environment variables` on the left side
1. Add the following environment variables, replacing the placeholders with the appropriate values

    ```sh
    DATABASE_URL=postgresql://postgres:<DB_PASSWORD>@<EC2_IP>:5432/postgres
    BASE_URL=https://<AMPLIFY_APP_URL> # Note: Do not include a trailing slash!
    GOOGLE_CLIENT_ID=<GOOGLE_CLIENT_ID>
    GOOGLE_CLIENT_SECRET=<GOOGLE_CLIENT_SECRET>
    ```

1. Click `Save`
1. Return to the app overview and click `main`
1. Click `Redeploy this version`
1. Wait for the deployment to complete
1. Visit the URL of the deployed app to see the project in action!
