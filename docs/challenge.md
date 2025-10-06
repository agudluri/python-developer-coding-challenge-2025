## Objective
Build a production-ready analytics platform for AWS VPC Flow Logs. Candidates will ingest raw logs from Amazon S3, process them with Python, visualize insights in Plotly Dash, and automate deployment with Docker, Terraform, and GitHub Actions targeting AWS services.

## Scope & Expectations
- You must use AWS as the primary cloud. Azure/GCP implementations are out of scope for this challenge.
- Treat this as a real-world engagement: infrastructure, automation, observability, and documentation should be ready for team hand-off.
- Assume reviewers will provision resources in their own AWS account by following your instructions.
- Complete the challenge within 3–4 days of receiving repository access.
- Follow only the instructions contained in this repository; disregard conflicting guidance from other channels.

## Functional Requirements
Your application must:
- Download and decompress zipped VPC Flow Log files stored in an S3 bucket.
- Parse each record to extract account, VPC/subnet/ENI identifiers, source/destination IPs and ports, protocol, action, bytes, packets, and timestamps.
- Aggregate data to highlight top talkers/listeners, common ports/services, denied traffic, and anomalies (spikes, long-lived connections, unusual regions).
- Power an interactive Plotly Dash interface with:
  - Top 10 source and destination IP bar charts.
  - Visualization of denied flows (bar or pie).
  - Time-series chart of flows per hour and complementary heatmap.
  - Gauge/bullet chart for total flows vs. denied percentage.
  - Tables summarizing top talkers/listeners.
  - Geo map of external IP activity (derive from GeoIP database or synthetic mapping).
  - Sankey diagram of IP-to-IP conversations.
  - Text metrics summarizing totals, anomaly windows, and resource usage.
- Support filtering by account, VPC, subnet, ENI, protocol, action, and time window.
- Expose a CLI entry point (`networkflow dashboard`) that pulls data from S3 and serves the Dash UI on port 8050.
- Provide containerized deployment (Docker image) with identical behavior locally and in AWS.

## Prerequisites
- Terraform, Docker, Python 3.10+, and the AWS CLI installed and authenticated (`aws sts get-caller-identity` succeeds).
- GitHub account that accepts a collaborator invite to this repository so you can push branches and open PRs.
- Ability to generate representative VPC Flow Logs data (see Data Requirements).

## Technical Deliverables
### 1. Python Package
- Create a `networkflow` package with at minimum:
  - `parsers.py` to read and decompress gzipped/plain text VPC Flow Log files from S3.
  - `analyzer.py` to compute aggregations, anomalies, and summary statistics.
  - `dashboard.py` to bootstrap the Dash app and register the CLI entry point:
    ```bash
    networkflow dashboard \
      --bucket <s3_bucket_name> \
      --prefix <logs_prefix> \
      [--aws-region <region>] \
      [--assume-role <role_arn>]
    ```
- Implement ≥ 3 pytest tests covering parser edge cases, retry/backoff behavior, and anomaly detection logic.
- Provide ≥ 1 test validating that the Dash app factory starts successfully (can use Dash test client or HTTP check against a test server).

### 2. Plotly Dash Application
- Serve the UI at `http://localhost:8050` and from the container on port 8050.
- Include the visualizations listed in Functional Requirements.
- Ensure filters interact smoothly (no full refresh required) and clearly highlight denied/anomalous flows.
- Add loading/error states for data retrieval issues (e.g., S3 connectivity).

### 3. Containerization
- Supply a `Dockerfile` that installs dependencies, copies source/tests, and sets an entry point (e.g., `networkflow dashboard ...`).
- Document local execution (e.g., `docker run --rm -p 8050:8050 -e S3_BUCKET=... networkflow`).
- Keep the final image < 200 MB.

### 4. Infrastructure as Code (`infra/` directory)
- Use Terraform to provision:
  - S3 bucket for flow-log archives (enable encryption, versioning optional but preferred).
  - AWS Lambda or AWS Glue job *(optional but encouraged)* if you need scheduled preprocessing.
  - Amazon ECR repository for container images.
  - AWS Fargate (ECS) service or AWS App Runner to run the dashboard.
  - IAM roles/policies granting least-privilege access (ECS task role for S3 read, CI/CD role, etc.).
  - CloudWatch Log Group (or equivalent) capturing application logs.
- Configure remote Terraform state in S3 with DynamoDB table for locking.
- Output values your reviewers need: `s3_bucket_name`, `s3_logs_prefix`, `ecr_repository_url`, `ecs_cluster_name`/`app_runner_service`, `service_url`, `iam_role_arns`.

### 5. CI/CD Automation
- Add `.github/workflows/ci.yml` triggered on pushes/PRs targeting `main` that:
  1. Installs dependencies and runs `pytest` with ≥ 80% coverage.
  2. Runs linting (`flake8` or `pylint`) with zero errors.
  3. Executes `terraform fmt -check`, `terraform init`, `terraform validate`, `terraform plan`, and `terraform apply --auto-approve` (use `-target` or workspaces if you separate environments).
  4. Builds the Docker image, tags it with the commit SHA, and pushes to ECR.
  5. Deploys/updates the ECS/App Runner service to use the new image.
- Use GitHub Actions OpenID Connect or encrypted secrets for AWS credentials; document required secrets in `README.md`.
- Cache dependencies where appropriate to keep build times reasonable.

### 6. Verification Tooling
- Implement `verify_resources.py` with CLI arguments:
  ```bash
  python verify_resources.py \
    --bucket <s3_bucket_name> \
    --prefix <logs_prefix> \
    --service <cluster_name/service_name> \
    --region <aws_region>
  ```
- Use Boto3 to confirm:
  - S3 bucket and prefix exist and are accessible.
  - ECS/App Runner service is running the expected task + image tag.
  - Optionally validate CloudWatch log group creation and basic health checks.
- Exit with non-zero status if validation fails; print friendly summary output for reviewers.

## Data Requirements
- No sample data is bundled. You must supply realistic VPC Flow Log records so reviewers can run the dashboard.
- Provide gzipped CSV files using the AWS VPC Flow Logs default format (version 2+ preferred):
  ```
  version account-id interface-id srcaddr dstaddr srcport dstport protocol packets bytes start end action log-status tcp-flags type pkt-srcaddr pkt-dstaddr pkt-src-aws-service pkt-dst-aws-service flow-direction packet-dstaddr region sublocation-id sublocation-type vpc-id subnet-id instance-id tcp-connection-status
  ```
- Expectations for your dataset:
  - ≥ 24 hours of traffic with at least two VPCs, multiple subnets, and diverse ENIs.
  - Mixture of `ACCEPT` and `REJECT` actions, including anomaly scenarios (e.g., port scans, exfiltration spikes).
  - Geo-diverse public IPs (consider using public datasets or synthetic values plus a GeoIP lookup).
  - Include connections across protocols (TCP, UDP, ICMP) and port ranges.
- Document how to regenerate the dataset:
  - If synthetic, commit the generator script (e.g., `tools/generate_flow_logs.py`) and usage instructions.
  - If anonymized from real logs, describe sanitization steps and provide access instructions (e.g., share via S3 pre-signed URL).

## Review & Submission Workflow
1. Accept the collaborator invite, clone the repo, and create a feature branch (`firstname-lastname-solution`).
2. Commit work frequently with descriptive messages.
3. Push your branch and open a PR against `main`. Tag your recruiting contact and include:
   - Links or screenshots for passing tests, linting, and Terraform plans/applies.
   - Deployment URLs (e.g., ECS service endpoint).
   - Instructions for accessing sample data if not committed.
4. Leave the PR open until we complete review; expect follow-up questions or requested tweaks.

## Evaluation Criteria
- **Data Handling:** Reliability and clarity of log ingestion, parsing, and enrichment.
- **Analytics Quality:** Accuracy and usefulness of insights, anomaly detection, and visualization UX.
- **Infrastructure & Automation:** Terraform structure, AWS security posture (least privilege, encryption), CI/CD robustness.
- **Code Quality:** Modularity, documentation, test coverage, and adherence to Python best practices.
- **Developer Experience:** Clarity of README/setup instructions, reproducibility, and ease of review.

Deliver your solution as if it were heading into production—polished, secure, and well-documented. Good luck!
