#### Job Description

**Python Developer – Cloud Infrastructure, Automation & Security Logging**
**Location:** Remote 
**Type:** Contract

##### ==About the Role==
We’re seeking a versatile Python Developer to design, build, and operate an end-to-end pipeline for ingesting, analyzing, and visualizing security logs across AWS, Azure, and GCP. You’ll enable our security and operations teams to surface actionable insights from DNS logs, Proxy logs, NSG flow logs, Orca, Uptycs, and more.

##### ==Key Responsibilities==
- **Multi-Cloud Log Ingestion & Analysis**  
  - Write Python code to fetch and normalize logs via AWS/Azure/GCP APIs (e.g., S3, Storage Queues, Pub/Sub) 
  - Parse, cleanse, and aggregate diverse log types (DNS, proxy, Orca, Uptycs, NSG flow logs, etc.)  
  - Identify data quality issues, annotate metadata, and document remediation steps  

- **Interactive Visualization**  
  - Build reusable **Plotly** Dash components (heatmaps, time-series, geospatial maps) that allow security teams to drill into anomalies  
  - Annotate key events and embed insights for non-technical stakeholders  

- **Infrastructure as Code**  
  - Develop Terraform modules to provision logging infrastructure in AWS (S3, Kinesis), Azure (Storage Accounts, Log Analytics), and GCP (Cloud Storage, Pub/Sub)  
  - Configure remote state backends with locking and integrate secrets in secure stores (Key Vault, Secrets Manager)  

- **Configuration Automation** (==Nice to have==) 
  - Create Ansible roles/playbooks to provision and configure Ubuntu (or container) environments, install dependencies, deploy code, and run analyses  
  - Securely manage service principal or IAM credentials via Ansible Vault or environment variables  

- **Security Best Practices**  
  - Apply least-privilege principles when assigning IAM/RBAC roles  
  - Understand threat models for log data streams (e.g., log injection, tampering, retention) and recommend hardening measures  
  - Collaborate with Ops to tune alert thresholds and response workflows  

##### ==Required Qualifications==
- 3+ years professional Python development experience  
- Demonstrated ability to work with AWS, Azure, and GCP SDKs/APIs for storage, messaging, and compute  
- Strong Plotly or similar interactive visualization skills  
- Proven Terraform expertise across at least two cloud providers, with remote state and secret management    
- Experience parsing and making sense of security logs (e.g., DNS queries, proxy logs, NSG flows, Orca/Uptycs outputs)  
- Familiarity with security concepts and best practices (RBAC, least privilege, log integrity, etc.)  
- Comfortable with Git-based workflows and CI/CD pipelines  

##### ==Preferred Qualifications==
- Prior experience building security or SIEM dashboards  
- Containerization (Docker) and orchestration (Kubernetes/EKS, etc) skills  
- Hands-on with monitoring/alerting tools (Prometheus, Grafana, etc)  
- Familiarity with mocking and testing frameworks (pytest, moto, vcrpy)  
- Bachelor’s degree in Computer Science, Engineering, or related field (or equivalent experience)  
