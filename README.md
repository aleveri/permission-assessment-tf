# GKE Terraform and Containerized API Service Helm Project

## Prerequisites

- [Google Cloud SDK](https://cloud.google.com/sdk/docs/install)
- [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)
- [Helm](https://helm.sh/docs/intro/install/)
- [Docker](https://docs.docker.com/get-docker/)
- A GCP account with billing enabled

## Setup Instructions

### 1. Configure GCP Project

1. Create a new GCP project.
2. Enable the Kubernetes Engine API and Compute Engine API.
3. Authenticate using the Google Cloud SDK:
    ```sh
    gcloud auth login
    gcloud config set project aleveri-assessment
    gcloud auth application-default login
    ```

### 2. Deploy GKE Cluster using Terraform

1. Clone the repository:
    ```sh
    git clone https://github.com/aleveri/permission-assessment-tf.git
    cd <repository-directory>
    ```

2. Initialize Terraform:
    ```sh
    terraform init
    ```

3. Apply the Terraform configuration:
    ```sh
    terraform apply -var 'project_id=aleveri-assessment' -var 'region=us-east1'
    ```

### 3. Set Up Helm

1. Install Helm if not already installed:
    ```sh
    curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
    ```

2. Initialize Helm and add any necessary repositories:
    ```sh
    helm repo add stable https://charts.helm.sh/stable
    helm repo update
    ```

### 4. Build Docker Image for API Service

1. Clone the repository:
    ```sh
    git clone https://github.com/aleveri/permission-assesment-api.git
    cd <repository-directory>
    ```

2. Build the Docker image:
    ```sh
    docker build -t apiservice:latest -f Dockerfile .
    ```

### 5. Deploy API Service using Helm

1. Deploy the application to the GKE cluster:
    ```sh
    helm install apiservice ./apiservice
    ```

### 6. Verify Deployment

1. Get the external IP of the service:
    ```sh
    kubectl get services
    ```

2. Script interactions with the API service to validate its functionality:
    ```sh
    curl http://<external-ip>:8080/health
    ```

### Cleanup

To destroy the resources created by Terraform:
```sh
terraform destroy
```

To uninstall the Helm chart:
```sh
helm uninstall apiservice
```

## Evaluation Criteria

### Technical Requirements (50%)

- **Infrastructure Setup**: GKE cluster configured correctly, Terraform code well-structured & follows best practices.
- **Application Deployment**: Helm chart deploys API service successfully, chart well-structured & follows best practices.
- **API Testing & Functionality**: Meaningful and thorough tests that validate API functionality.

### Documentation (50%)

- **README Clarity & Completeness**: Clear, concise, easy-to-follow instructions, troubleshooting tips, logical flow.
- **Written Communication**: Professional tone, correct grammar/spelling, effective technical communication.

If you run out of time and skip anything, please explain why and what you would do if you had more time to complete the test.
