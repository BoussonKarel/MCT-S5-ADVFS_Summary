# DevOps
- Implementing a **Continues Integration** pipeline
  - Triggering on **Git** pushes / merges / pull requests
  - Automated Docker build, tag and push
- Implementing a **Continuous Deployment** pipeline
  - Fully automated
  - **Kubernetes** deployment
  - **Zero-downtime**

## CI & CD
![picture 5](../images/aaafc2f50f2bc031cfef2ee4d3eafcb0b069ae03783bf34cd035f3a73bdadd93.png)  

- **CI** = **Continuous Integration**
- **CD** =
  - **Continuous Delivery**
    - Wachten tot we manueel toestemming geven om te deployen naar productie.
  - **Continuous Deployment**

### Pre-phase
- Initiate a **trigger**
  - Pull-request
  - From another pipeline
  - Manual
  - Scheduled (daily, weekly, monthly...)
- Source
  - Pulling the Git repository
  - Gathering more data (external data sources...)

### Builds
- Compiling programs (Java, Go...)
- Package installations
  - pip install ...
  - npm ci
- Docker builds

### Tests
- Unit tests
- Integration tests
- Code Coverage
- Cyclomatic Complexity: How complex is my code? Loops, clauses...

### Acceptance tests
- Is my project complete?
- Is it acceptable?

### Deploy to staging
- Deploy to a staging environment where more checks can happen
- Similar hardware as production environment
- **Not equal** to a Development environment
- **One-click** away from production
  - **Only** when talking about **continuous delivery**

### Deploy to production
- Deploying to the public
- Kubernetes deployment
- Zero-downtime
+ **Green-blue** deployment
+ **Canary** deployment
- Automatic deployment when **continuous deployment** is configured
- Manual deployment when **continuous delivery** is configured

### Deploy to production: Green-blue deployment
Switch the one available to public
![picture 6](../images/c7546a6391d630aa09aca05344e99be65f53b68bf96cf999a64b1f1f2d71ad4b.png)  

![picture 7](../images/e0e14968ada956baf29daf763d5a6130e124cda60d74835bf92a487b181324d5.png)  

Je maakt de staging aan, je bouwt en dan switch je naar die versie, dan verwijder je de oude production.

### Deploy to production: Canary deployment
- Roll-out your service to a small portion of users
- Roll-back if necessary

![picture 8](../images/78700f639956d32b9f7ae407f60a1cec50d3044e2ecfe4d64f73704493eb708f.png)  

![picture 9](../images/64b411b46e52f927a3acbeb3f7f08ae676dfa12f6deac8a8f243d1b4c3cc5914.png)  

Monitoren van de enkele gebruikers, daarna ook de rest updaten.

![picture 10](../images/ec7fa99fc3b6398f52043f12ebcf67065c7a9917eb8876a35673a6a3e2e49798.png)  

*Bv. Facebook met nieuwste features voor sommige.*

### Monitoring
- Keep track of the health of your services
- Track the load, traffic...

## CI/CD Tools
### CI/CD Tools
- Azure DevOps - Azure Pipelines
- GitHub - GitHub Actions
- GitLab - GitLab CI/CD
- Rancher - Rancher Pipelines

### Local runners
- We only want local Runners, so we can deploy to a local Kubernetes cluster
- Github Actions self-hosted Runner
- GitLab Runner
- Azure Pipelines Agent

*Enkel binnen Howest netwerk kunnen we met de Kubernetes cluster werken.*

### GitHub Actions
- Triggered trough different options
- There is a whole **marketplace** of available actions
- **Azure CLI tasks**

### GitHub Actions: YAML

### GitHub Actions: Flows
- Multiple Workflows
  - Name them accordingly
  - Refer to them by their names, so you can trigger them from another one
- Shared workflows

### GitHub Actions: Triggers
- Webhooks (a POST request with a body)
- Repository pushes
  - Everytime the codebase changes
- Manual trigger

```yaml
on:
  push:
    branches: [main, develop]
```

![picture 12](../images/335010c8ca1c7e98e45cd8a0e3edddbc60261a3b5b6103098bcf66f577820e77.png)  

### Github Actions: Secrets
- We can use Repository variables and **secrets** into our Github Actions flow

![picture 13](../images/3fc3c544c4c2df94e41e7fa6178ef0a8af9db65fcb3c4fa7dffa9ca6c1c52c06.png)  

## Summary
- How to build a CI pipeline with GitHub Actions
- How to build a CD pipeline with GitHub Actions
- How to automatically deploy Kubernetes micro-service applications with GH Actions
- What are the different deployment strategies?
- How to work with GH Actions?