# Platform CD

This repository is part of my **DevOps CI/CD portfolio project**, designed to demonstrate my practical knowledge and hands-on experience in designing and implementing end-to-end **Continuous Delivery (CD)** workflows.
The goal of this project is to **showcase modern DevOps principles** — including environment promotion, automation, Kubernetes-based deployments, and release governance and references to my favorite DevOps Materials.

The application deployed through this repository comes from the companion repository **[microservices-app](https://github.com/lordpangan/microservices-app)** — a dummy Java microservices system. This repository covers the **Continuous Integration (CI)** side — including builds, tests, and image publishing — while this **platform-cd** repository focuses on the **Continuous Delivery and deployment orchestration** aspect.

---
### TODO:
- Add requirement for the ci-runner(what are the tools needed on the ci-runner)
    - crane
    - kubectl
    - npm
    - gh
- need to handle multiple app deployment per run
- We need a mechanism to redeploy if there are changes to k8s config and no app changes
- on manual run its easy to mispell or mistype the services
- Document branching strategy, feature flow, and release candidate promotion process.
- Add references to *Continuous Delivery* principles implemented in both `microservices-app` and `platform-cd`.

### Tech Stack

| Category | Tools / Technologies |
|-----------|----------------------|
| CI/CD Orchestration | **GitHub Actions** |
| Kubernetes Configuration Management | **Kustomize** |
| Scripting & Automation | **Bash** |
| Deployment Targets | **Kubernetes namespaces** (`sit`, `staging`, `prd`, `perf`) |
| Artifact Registry | **GitHub Container Registry (GHCR)** |

---

### Repository Overview
```
platform-cd/
├── .github/workflows/ # CD workflows for each environment
├── ops/
│ └── k8s/
│ ├── base/ # Base manifests per microservice
│ └── overlays/ # Environment-specific configs (SIT, STG, PRD, PERF)
└── test/
└── uat/ # Postman smoke tests and environment configs
```

---

### Environment Flow

| Environment | Purpose | Trigger | Notes |
|--------------|----------|----------|--------|
| **SIT** | Automated deployment for system integration testing | CI dispatch event | Runs Postman smoke tests |
| **STAGING** | Manual promotion after SIT | Manual GitHub Action trigger | For UAT and exploratory testing |
| **PERF** | Optional non-functional testing | Manual | Load/performance validation |
| **PROD** | Final production deployment | Manual + approvals | Requires release candidate verification |
