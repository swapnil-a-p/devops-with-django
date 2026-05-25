# AWS Deployment Notes

This repository is intentionally lightweight, but it can still be used to demonstrate a practical AWS deployment path for a containerized Django application.

## Suggested Target Architecture

- GitHub repository as source control
- GitHub Actions for build and validation
- Amazon ECR for image storage
- Amazon ECS Fargate for container runtime
- Application Load Balancer for ingress
- Amazon CloudWatch for logs and metrics
- AWS Systems Manager Parameter Store or Secrets Manager for runtime configuration
- Amazon RDS PostgreSQL for a production database if the application evolves beyond SQLite

```mermaid
flowchart LR
    classDef source fill:#eef6ff,stroke:#4d8dff,color:#133768,stroke-width:2px;
    classDef pipeline fill:#18324d,stroke:#67c5ff,color:#eefbff,stroke-width:2px;
    classDef runtime fill:#17382c,stroke:#63d3a0,color:#effff7,stroke-width:2px;
    classDef infra fill:#2e243d,stroke:#c59aff,color:#fbf3ff,stroke-width:2px;
    classDef data fill:#3b2f16,stroke:#ffca6b,color:#fff8eb,stroke-width:2px;

    GH[GitHub]
    ACT[GitHub Actions]

    subgraph AWS[Target AWS Environment]
        ECR[Amazon ECR]
        ALB[Application Load Balancer]
        ECS[Amazon ECS Fargate]
        CW[CloudWatch]
        SEC[Secrets Manager /<br/>Parameter Store]
        RDS[(Amazon RDS PostgreSQL)]
    end

    GH --> ACT
    ACT --> ECR
    ECR --> ECS
    ALB --> ECS
    ECS --> CW
    SEC --> ECS
    ECS --> RDS

    class GH source;
    class ACT pipeline;
    class ECS runtime;
    class ECR,ALB,CW,SEC infra;
    class RDS data;
```

## Recommended Deployment Flow

1. Developer pushes to `main`
2. GitHub Actions builds and validates the container image
3. Image is pushed to Amazon ECR
4. ECS service is updated to deploy the new task definition
5. ALB routes traffic to the updated Fargate tasks

## Production Gaps To Address

- move from SQLite to a managed database
- replace the Django development server with Gunicorn
- inject secrets via environment variables or AWS managed secrets
- add health checks, container readiness, and structured logging
- introduce IaC for the runtime environment
