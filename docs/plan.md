# Plan

Each phase ends with a short "how it works" note and a git tag, so the project can be walked through phase by phase.
The generator and the analysis are built locally first, at zero cloud cost.

| # | Phase | What we build | What it proves |
|---|---|---|---|
| 0 | Foundations | Repo, README, plan, decision log, local tools | Organised project |
| 1 | Platform and permissions | Terraform: state storage, resource groups, ADLS, Key Vault, Databricks workspaces, Access Connectors, Unity Catalog catalogs / schemas / volumes / grants, service principals with GitHub OIDC, budget alerts | Infrastructure as code, least privilege |
| 2 | Data into the cloud | Generator as the "on-prem source system" uploading daily files; optional Data Factory copy; Auto Loader into bronze | Ingestion, moving data between services |
| 3 | Transformation | Lakeflow pipeline bronze -> silver -> gold with data quality checks and quarantine | Data engineering |
| 4 | Analytics | Churn drivers, cohort retention, revenue at risk, dashboard on gold | Analytical thinking |
| 5 | Modelling | Baseline -> gradient boosting, time-based split, calibration, MLflow, Unity Catalog registry, champion / challenger gate | Sound ML |
| 6 | Decision | Uplift + budget optimizer, profit vs random and top-N targeting | Business value |
| 7 | Deployment | Scheduled batch scoring in prod; optional real-time endpoint | Model deployment |
| 8 | CI/CD | GitHub Actions: checks on PR, dev deploy, prod deploy on tag with approval; Terraform plan / apply | Automation |
| 9 | Monitoring | Feature and prediction drift, accuracy once outcomes arrive, alerts, retraining trigger | Production ownership |
| 10 | Failure scenarios | Scripted break-and-fix demos | Handling problems |
| 11 | Show it off | 15-minute README, architecture diagram, screenshots, video, X article | Communication |

## Environments

- Two environments: `dev` and `prod`.
- Each has its own resource group, storage account and Databricks workspace.
- Unity Catalog: catalog per environment (`churn_dev`, `churn_prod`), schema per layer (`landing`, `bronze`, `silver`, `gold`, `ml`).
- Everything is temporary: built with `make up`, deleted with `make down`.

## Cost (rough)

- About 1 EUR per hour of compute while working.
- About 3-6 EUR for a 2-4 hour session when the environment is built and deleted each time.
- Local phases cost nothing.
