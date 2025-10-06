# Python Developer – Cloud Infrastructure, Automation & Security Logging

**Location:** Remote  
**Type:** Contract

## About the Role
We are looking for a versatile Python developer to design, build, and operate an end-to-end pipeline for ingesting, analyzing, and visualizing security logs across AWS, Azure, and GCP. You will help our security and operations teams surface actionable insights from DNS logs, proxy logs, NSG flow logs, VPC flow logs, Orca, Uptycs, and additional telemetry sources.

## Key Responsibilities
### Multi-Cloud Log Ingestion & Analysis
- Write Python services to fetch and normalize logs via AWS/Azure/GCP APIs (S3, Storage Accounts, Google Cloud Storage, etc.).
- Parse, cleanse, and aggregate diverse log types (DNS, proxy, Orca, Uptycs, NSG flow logs, VPC flow logs, and more).
- Identify data quality issues, annotate metadata, and document remediation steps.

### Interactive Visualization
- Build reusable Plotly Dash components (heatmaps, time-series, geospatial maps) that let security teams drill into anomalies.
- Annotate key events and embed insights for non-technical stakeholders.

### Infrastructure as Code
- Develop Terraform modules to provision logging infrastructure in AWS (S3, SQS), Azure (Storage Accounts, Log Analytics), and GCP (Cloud Storage, Pub/Sub).
- Configure remote state backends with locking and integrate secrets with secure stores (Key Vault, Secrets Manager, etc.).

### Security Best Practices
- Apply least-privilege principles when assigning IAM/RBAC roles.
- Understand threat models for log data streams (log injection, tampering, retention) and recommend hardening measures.
- Collaborate with Operations to tune alert thresholds and response workflows.

## Required Qualifications
- 3+ years of professional Python development experience.
- Demonstrated ability to work with AWS, Azure, and GCP SDKs/APIs for storage, messaging, and compute services.
- Strong Plotly (or comparable interactive visualization) skills.
- Proven Terraform expertise, including remote state and secret management.
- Experience parsing and deriving insights from security logs (DNS queries, proxy logs, NSG flows, Orca/Uptycs outputs, etc.).
- Familiarity with security concepts and best practices (RBAC, least privilege, log integrity, etc.).
- Comfortable with Git-based workflows and CI/CD pipelines.

## Preferred Qualifications
- Prior experience building security or SIEM dashboards.
- Containerization (Docker) and orchestration (Kubernetes/EKS, etc.) skills.
- Hands-on experience with monitoring and alerting tools (Prometheus, Grafana, etc.).
- Familiarity with mocking and testing frameworks (pytest, moto, vcrpy).
- Bachelor’s degree in Computer Science, Engineering, or a related field (or equivalent experience).
