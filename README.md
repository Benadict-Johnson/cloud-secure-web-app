# Cloud-Based Secure Web Application with DevSecOps Implementation

A secure, scalable, and highly available containerized web application deployed on AWS using DevSecOps best practices. The infrastructure isolates the application layer within a private network tier, leveraging automated pipelines for continuous security auditing and deployment.

## 🏗️ Project Architecture Overview

* **Network Segmentation:** Built within a custom AWS VPC utilizing distinct public and private subnets to enforce defense-in-depth isolation.
* **Traffic Ingress:** External user traffic terminates securely at an upstream Application Load Balancer (ALB) in the public subnet, which proxies requests down to an isolated EC2 Instance hosting an Nginx reverse proxy.
* **Identity & Access Management:** Avoids hardcoded credentials by using native IAM Instance Profile Roles to securely grant programmatic permissions to resources such as Amazon S3.

## 🛡️ Security & DevSecOps Practices

* **Static Application Security Testing (SAST):** Integrated automated security scanning utilizing Bandit within the continuous integration lifecycle to intercept vulnerabilities (e.g., debug modes) prior to production deployment.
* **Automated Logging & Telemetry:** Configured an active Amazon CloudWatch Agent daemon tracking real-time Nginx application access logs for continuous monitoring and operational observability.
* **State Durability:** Implemented an automated shell backup utility executing via Linux system cron schedules to push compressed application states directly to a secure Amazon S3 Bucket.

## 🚀 Repository Structure

```text
├── .github/
│   └── workflows/
│       └── deploy.yml          # CI/CD Pipeline Workflow (SAST Scan & Native Deployment)
├── src/                        # Main Web Application Source Code
└── README.md                   # Project Documentation

## 🛠️ Deployment Workflow Setup Instructions

### 1. Environment Configurations
Ensure your target EC2 instance has Docker, Nginx, and the Amazon CloudWatch Agent installed. Update directory permissions for the telemetry logger:
```bash
sudo chmod +rx /var/log/nginx
Initialize the local CloudWatch Agent lifecycle by pointing it to your runtime configuration file parameters:

Bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m e
Register a GitHub Actions Self-Hosted Runner on the deployment server target to securely process your production workflows.
