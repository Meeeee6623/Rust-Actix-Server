# Rust Actix Server Example

This project demonstrates a simple REST API server using Rust with the Actix web framework. It is containerized using Docker, automatically built and pushed to AWS Elastic Container Registry (ECR) through GitHub Actions, and deployed to AWS App Runner for easy scaling and management.

## Prerequisites

- Rust and Cargo
- Docker and Docker Compose
- AWS CLI configured with administrator access
- GitHub account

## Local Development

1. **Clone the repository**

    ```bash
    git clone https://github.com/yourusername/rust-actix-server.git
    cd rust-actix-server
    ```

2. **Build and run with Docker Compose**

    ```bash
    docker-compose up --build
    ```

    This command builds the Docker container and starts the server. The API will be available at `http://localhost:8080`.

## Deployment

1. **Set up AWS ECR:**

    Create an ECR repository if you haven't already:

    ```bash
    aws ecr create-repository --repository-name rust-actix-server --region your-region
    ```

2. **Configure GitHub Secrets:**

    Add the following secrets to your GitHub repository to use in the GitHub Actions workflow:
    - `AWS_ACCESS_KEY_ID` - Your AWS access key.
    - `AWS_SECRET_ACCESS_KEY` - Your AWS secret access key.

3. **GitHub Actions Workflow**

    The `.github/workflows/aws_deploy.yml` file contains the GitHub Actions workflow to automate the deployment process. It builds the Docker image, pushes it to ECR, and triggers a deployment in App Runner when changes are pushed to the main branch.

## GitHub Actions Workflow Explanation

- **Build and Push to ECR:**
  This step builds the Docker image from the Dockerfile, logs in to AWS ECR, and pushes the built image to ECR.

- **Deploy to AWS App Runner:**
  Using the new image in ECR, this step updates the AWS App Runner service to deploy the new version of the application automatically.

## Additional Notes

- Ensure your AWS App Runner service is set up to pull from your ECR repository.
- Modify the `docker-compose.yml` and `Dockerfile` as necessary to match your project requirements.
