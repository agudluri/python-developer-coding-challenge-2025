# Python Developer Coding Challenge

Welcome! This repository gives you everything you need to decide if the role fits your skills and to complete the technical exercise.

## How to Navigate
- Review the [job description](docs/job-description.md) to understand the team, responsibilities, and skills we value.
- Read the [coding challenge](docs/challenge.md) for detailed requirements, deliverables, and evaluation criteria.
- Accept the collaborator invitation we send you so you can push directly to this repository.
- Follow the submission guidance below to commit your work.

## AWS Focus
This hiring challenge is AWS-specific. Your solution must target AWS services (S3, ECR, ECS, etc.) and operate on AWS VPC Flow Logs. Other clouds are out of scope.

## Timeline & Communication
- You have 3–4 days from when you receive repository access to complete and submit your solution.
- Follow the instructions in this repository exclusively, ignore conflicting guidance from other sources.

## Repository Structure
- `docs/job-description.md` — role overview and qualifications.
- `docs/challenge.md` — challenge specification, deliverables, and submission checklist.

## Data Expectations
- This repository does not include sample AWS VPC Flow Logs. You must supply representative data for your solution.
- Follow the guidance in [`docs/challenge.md`](docs/challenge.md#data-requirements) to generate gzipped CSV files that follow the AWS flow-log schema.
- Check your data into your branch only if it is synthetic and reasonably small, otherwise document the storage location and regeneration steps.

## Cost Tips
- The challenge can be completed within the AWS Free Tier. See [`docs/challenge.md`](docs/challenge.md#cost--free-tier-guidance).

## How to Submit
1. Accept the GitHub collaborator invitation from us (message your recruiting contact from DXC if you have not received one).
2. Clone this repository and create a feature branch named `firstname-lastname-solution`.
3. Commit your work with clear messages as you progress.
4. Push the branch to this repository and open a pull request into `main`.
5. Add build/test screenshots or links in the PR description.
6. Leave the branch and PR open until we confirm that the review is complete.

We recommend reviewing both documents before you start coding. If questions come up, reach out to your recruiting contact so we can clarify expectations quickly.
