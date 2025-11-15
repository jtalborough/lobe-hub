# LobeChat Docker Compose for Portainer

This repository contains a `docker-compose.yml` file to deploy LobeChat using Portainer.

## Setup

1.  **Fork this repository** to your GitHub account.
2.  **In Portainer**, go to "Stacks" and click "Add stack".
3.  **Select "Git repository"** as the deployment method.
4.  **Enter the URL** of your forked repository.
5.  **Set the Compose path** to `docker-compose.yml`.
6.  **Click "Deploy the stack"**.

## Configuration

Before deploying, you will need to provide your secrets as environment variables in the Portainer UI.

Refer to the `.env.example` file for a complete list of required and optional environment variables. When deploying the stack, navigate to the **Environment variables** section in the Portainer UI and add the variables you need.

### Required Variables

-   `OPENAI_API_KEY`: Your OpenAI API key.
-   `CLOUDFLARE_TUNNEL_TOKEN`: Your Cloudflare Tunnel token.
-   `POSTGRES_PASSWORD`: A strong, unique password for the PostgreSQL database.
-   `KEY_VAULTS_SECRET`: A long, random, and secret string for encrypting credentials. You can generate one with `openssl rand -base64 32`.
-   `NEXT_AUTH_SECRET`: A long, random, and secret string for NextAuth. You can generate one with `openssl rand -hex 32`.

### SSO Provider Variables

You must configure at least one SSO provider.

-   `NEXT_AUTH_SSO_PROVIDERS`: A comma-separated list of the providers you want to enable (e.g., `github`, `google`).

#### Example: GitHub SSO

If you use GitHub, you need to provide the following:

-   `AUTH_GITHUB_ID`: Your GitHub OAuth App's Client ID.
-   `AUTH_GITHUB_SECRET`: Your GitHub OAuth App's Client Secret.

### Optional: S3 Object Storage

These variables are only needed if you want to use an S3-compatible service (like Cloudflare R2 or AWS S3) for file storage. **If you do not configure this, you must remove these variables entirely from your Portainer stack, otherwise the application will fail to start.**

-   `S3_ACCESS_KEY_ID`: Your S3 access key.
-   `S3_SECRET_ACCESS_KEY`: Your S3 secret key.
-   `S3_ENDPOINT`: The endpoint URL of your S3 service.
-   `S3_BUCKET`: The name of your S3 bucket.
-   `S3_PUBLIC_DOMAIN`: The public-facing URL for accessing files in your bucket.
