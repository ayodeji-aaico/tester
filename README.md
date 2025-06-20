flowchart TD
  subgraph GitHub
    GH1[Source Code Repos]
    GH2[GitHub Actions]
    GH3[GitHub Apps]
  end

  subgraph CI/CD
    GH2 --> Build[Build & Push Docker Images to ECR]
    Build --> ECR[(AWS ECR)]
  end

  subgraph GitOps
    GH1 --> Flux[FluxCD]
    Flux --> K8s[Kubernetes Cluster]
    Flux --> GitOpsCommit[Image Tag Updates via Commit]
  end

  subgraph AWS IaC
    Crossplane[Crossplane Controllers]
    Crossplane --> AWS_S3[S3]
    Crossplane --> AWS_RDS[RDS]
    Crossplane --> AWS_SNS[SNS]
    Crossplane --> AWS_SQS[SQS]
    Crossplane --> AWS_IAM[IAM Roles/Policies]
    Crossplane --> AWS_ECR[ECR]
  end

  GitOpsCommit --> GH1
  Flux --> Crossplane
