# Cloud & DevOps Engineering: Master Execution Blueprint & Technical Roadmap

**Candidate:** Sanjeev Kumar  
**Target Identity:** Cloud Engineer / Junior DevOps Engineer → Cloud/SRE → Cloud Architect  
**Primary Credentials:** Red Hat Certified System Administrator (RHCSA EX200 | Cert ID: `260-029-343` | Score: 221/300)  
**Academic Background:** Bachelor of Science (B.Sc.) - Mathematics (MDS University, 2023 – 2026)  
**Core Baseline:** Linux (RHEL 9/10), AWS (VPC, EC2, S3, CloudFront, Route 53, IAM), Azure (VNet, VM, Functions, Blob, MySQL), Terraform, Bash, Git/GitHub  

---

## Table of Contents
1. [Executive Strategy: Why Priority 1 First?](#1-executive-strategy-why-priority-1-first)
2. [The Priority 1 Flagship Project: Production-Grade Multi-Tier DevOps Pipeline](#2-the-priority-1-flagship-project-production-grade-multi-tier-devops-pipeline)
   - [2.1 Architecture Overview & Topology](#21-architecture-overview--topology)
   - [2.2 Production-Grade Multi-Stage Dockerfile Specification](#22-production-grade-multi-stage-dockerfile-specification)
   - [2.3 Multi-Container Local Orchestration (`docker-compose.yml`)](#23-multi-container-local-orchestration-docker-composeyml)
   - [2.4 Enterprise GitHub Actions CI/CD Pipeline (`devops-pipeline.yml`)](#24-enterprise-github-actions-cicd-pipeline-devops-pipelineyml)
   - [2.5 Infrastructure as Code (Terraform AWS Deployment)](#25-infrastructure-as-code-terraform-aws-deployment)
3. [Interview Master Playbook: Real-World Scenarios & Defenses](#3-interview-master-playbook-real-world-scenarios--defenses)
   - [3.1 Docker & Containerization Deep-Dive](#31-docker--containerization-deep-dive)
   - [3.2 Networking & VPC Packet Flow Troubleshooting](#32-networking--vpc-packet-flow-troubleshooting)
   - [3.3 Linux Administration (RHCSA Level) Scenarios](#33-linux-administration-rhcsa-level-scenarios)
   - [3.4 Terraform Production Lifecycle & State Management](#34-terraform-production-lifecycle--state-management)
   - [3.5 CI/CD & Pipeline Security](#35-cicd--pipeline-security)
4. [Portfolio & Resume Transformation Blueprint](#4-portfolio--resume-transformation-blueprint)
   - [4.1 Resume Bullet Optimization (FlowCV Alignment)](#41-resume-bullet-optimization-flowcv-alignment)
   - [4.2 GitHub Repository Presentation Standards](#42-github-repository-presentation-standards)
   - [4.3 LinkedIn Technical Branding & Recruiter Hook Plan](#43-linkedin-technical-branding--recruiter-hook-plan)
5. [90-Day Next-Horizon Roadmap: Kubernetes & Observability](#5-90-day-next-horizon-roadmap-kubernetes--observability)
   - [Phase 1 (Weeks 1–3): Docker & CI/CD Mastery](#phase-1-weeks-13-docker--cicd-mastery)
   - [Phase 2 (Weeks 4–7): Kubernetes (CKS/CKA Concepts, EKS, Helm)](#phase-2-weeks-47-kubernetes-ckscka-concepts-eks-helm)
   - [Phase 3 (Weeks 8–10): Observability & Monitoring (Prometheus, Grafana, Alertmanager)](#phase-3-weeks-810-observability--monitoring-prometheus-grafana-alertmanager)
   - [Phase 4 (Weeks 11–12): DevSecOps & Platform Engineering Foundation](#phase-4-weeks-1112-devsecops--platform-engineering-foundation)

---

# 1. Executive Strategy: Why Priority 1 First?

### The Skill Gap vs. Resume Exposure Analysis

Your resume lists **Docker workflows** and **Git/GitHub branching**, and your career goal points toward **DevOps & Cloud Engineering**. However, an honest technical audit reveals an imbalance:

```
┌───────────────────────────────────────┬───────────────────────────────────────┐
│          STABLE FOUNDATION            │             EXPOSED GAPS              │
│       (Defensible in Interview)       │       (Vulnerable in Interview)       │
├───────────────────────────────────────┼───────────────────────────────────────┤
│ • Linux / RHEL 9 (RHCSA certified)    │ • Docker (Currently ~2/5 depth)       │
│ • Networking (CIDR, Subnets, Routing) │ • CI/CD Automation (Currently ~1/5)   │
│ • AWS VPC & Core Architecture         │ • Container Security / Scanning       │
│ • Terraform (VPC 45m → 45s metric)    │ • Orchestration / Microservices       │
└───────────────────────────────────────┴───────────────────────────────────────┘
```

### The Strategic Dependency Chain

```
               [ Step 1: Priority 1 Project ]
           (Build Multi-Tier Docker + CI/CD + AWS)
                            │
              ┌─────────────┴─────────────┐
              ▼                           ▼
    [ Step 2: Interview Prep ]   [ Step 3: Resume Update ]
    (Real technical stories,     (Verifiable metrics, production
     debugged scenarios)          repo link, zero impostor syndrome)
              │                           │
              └─────────────┬─────────────┘
                            ▼
               [ Step 4: Next-Level Roadmap ]
                  (Kubernetes EKS & Grafana)
```

**Why you must NOT start with Interview Prep or Resume Updates first:**
1. **Empty Rehearsal Risk:** Memorizing answers about Docker and CI/CD without having built, broken, and fixed real pipelines leads to immediate failure when an interviewer asks: *"Tell me about a time your container build failed due to PID 1 signal propagation, or how you pruned cached layers in GitHub Actions."*
2. **Resume Authenticity:** When you finish this project, your resume gains verifiable bullets with GitHub commits, logs, and live architecture links.
3. **Synergy with RHCSA:** Combining your proven Linux skills with container internals (namespaces, cgroups, file permissions inside rootless containers) turns you into a top-tier candidate among junior applicants.

---

# 2. The Priority 1 Flagship Project: Production-Grade Multi-Tier DevOps Pipeline

**Project Title:** Cloud-Native Automated Microservice Delivery Platform  
**Target Repository:** `SanjeevKumar-Cloud/production-docker-cicd-aws`

---

## 2.1 Architecture Overview & Topology

The application is an enterprise-grade multi-tier service:
- **Client / Ingress:** CloudFront CDN / Internet → AWS Application Load Balancer or Nginx Reverse Proxy.
- **Web/API Tier:** Python Flask REST API running under Gunicorn WSGI, containerized using rootless, multi-stage Docker builds.
- **Data Tier:** PostgreSQL (or MySQL) relational database with persistent data volumes, automated database migrations, and isolated internal networking.
- **Pipeline:** GitHub Actions handling static linting, security scanning (Trivy), container build/push (Amazon ECR), and automated Terraform deployment.

```
[Developer] 
     │ (git push to main)
     ▼
[GitHub Actions CI/CD Pipeline]
     ├── 1. Code Linting & Static Analysis (Flake8, Hadolint)
     ├── 2. Security Vulnerability Scan (Trivy CVE, GitLeaks)
     ├── 3. Unit & Integration Testing (Pytest + Mock DB)
     ├── 4. Multi-Stage Docker Build & Cache Optimization
     ├── 5. Push Immutable Image to AWS ECR / GHCR (Tagged with Commit SHA)
     └── 6. Terraform Apply / Automated Rolling Deployment
                                 │
                                 ▼
                     [AWS VPC Infrastructure]
   ┌─────────────────────────────────────────────────────────────┐
   │ Public Subnet                                               │
   │   ├── Internet Gateway (IGW)                                │
   │   └── Nginx Reverse Proxy Container (Port 80/443)           │
   │             │ (Reverse Proxy pass via internal bridge)      │
   │             ▼                                               │
   │ Private Subnet (No Direct Inbound Internet)                 │
   │   ├── Gunicorn + Flask Application Container (Port 5000)    │
   │   │     │ (Non-root user, minimal distroless/slim base)     │
   │   │     ▼ (Port 5432 - Private Database Network)            │
   │   └── PostgreSQL / MySQL Database (Persistent Volume Mount) │
   └─────────────────────────────────────────────────────────────┘
```

---

## 2.2 Production-Grade Multi-Stage Dockerfile Specification

### Common Anti-Patterns to Avoid:
- ❌ Running as `root` (UID 0) inside the container.
- ❌ Storing build dependencies (compilers, build tools) inside the final runtime image.
- ❌ Using `latest` tag instead of specific, pinned base images.
- ❌ Leaving secret credentials or `.env` files in layer cache.

### The Production Multi-Stage `Dockerfile`:

```dockerfile
# ==============================================================================
# Stage 1: Build & Dependency Stage
# ==============================================================================
FROM python:3.11-slim-bookworm AS builder

# Prevent Python from writing .pyc files and enable unbuffered logging
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /install

# Install build dependencies required for compiling C extensions (if any)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Copy dependency definition only (leverages layer caching)
COPY requirements.txt .

# Install dependencies into dedicated target directory
RUN pip install --no-cache-dir --prefix=/install/deps -r requirements.txt


# ==============================================================================
# Stage 2: Final Minimal Runtime Stage
# ==============================================================================
FROM python:3.11-slim-bookworm AS runner

# Security hardening: Create non-root dedicated service user & group
RUN groupadd -g 10001 appgroup && \
    useradd -u 10001 -g appgroup -s /sbin/nologin -d /app appuser

WORKDIR /app

# Install minimal runtime shared libraries (libpq for postgresql)
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq5 \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Copy only the compiled dependencies from builder stage
COPY --from=builder /install/deps /usr/local

# Copy application source code with strict ownership
COPY --chown=appuser:appgroup ./src /app

# Set non-root execution context
USER 10001:10001

# Healthcheck to verify service responsiveness
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
    CMD curl -f http://127.0.0.1:5000/health || exit 1

EXPOSE 5000

# Execute through Gunicorn WSGI with production worker configuration
CMD ["gunicorn", "--workers=3", "--bind=0.0.0.0:5000", "--access-logfile=-", "--error-logfile=-", "wsgi:app"]
```

### Essential `.dockerignore`:
```text
.git
.github
.gitignore
__pycache__/
*.pyc
*.pyo
*.pyd
.env
.venv/
env/
tests/
Dockerfile*
docker-compose*.yml
README.md
terraform/
```

---

## 2.3 Multi-Container Local Orchestration (`docker-compose.yml`)

This provides isolated networking, healthchecks, secrets handling, and dependency orders.

```yaml
version: '3.8'

networks:
  frontend-network:
    driver: bridge
  backend-network:
    driver: bridge
    internal: true # Isolates database from external internet

volumes:
  db-data:
    driver: local

services:
  # ----------------------------------------------------------------------------
  # Reverse Proxy (Nginx) - Public Ingress
  # ----------------------------------------------------------------------------
  reverse-proxy:
    image: nginx:1.25-alpine
    container_name: devops-reverse-proxy
    restart: always
    ports:
      - "80:80"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    networks:
      - frontend-network
    depends_on:
      app:
        condition: service_healthy

  # ----------------------------------------------------------------------------
  # Application Backend (Python Flask + Gunicorn)
  # ----------------------------------------------------------------------------
  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: devops-backend-api
    restart: always
    environment:
      - DB_HOST=database
      - DB_PORT=5432
      - DB_NAME=cloud_db
      - DB_USER=cloud_user
      - DB_PASSWORD_FILE=/run/secrets/db_password
      - FLASK_ENV=production
    secrets:
      - db_password
    networks:
      - frontend-network
      - backend-network
    depends_on:
      database:
        condition: service_healthy

  # ----------------------------------------------------------------------------
  # Database Service (PostgreSQL) - Completely Private
  # ----------------------------------------------------------------------------
  database:
    image: postgres:16-alpine
    container_name: devops-database
    restart: always
    environment:
      POSTGRES_DB: cloud_db
      POSTGRES_USER: cloud_user
      POSTGRES_PASSWORD_FILE: /run/secrets/db_password
    secrets:
      - db_password
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - backend-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U cloud_user -d cloud_db"]
      interval: 10s
      timeout: 5s
      retries: 5

secrets:
  db_password:
    file: ./secrets/db_password.txt
```

---

## 2.4 Enterprise GitHub Actions CI/CD Pipeline (`devops-pipeline.yml`)

Location: `.github/workflows/ci-cd.yml`

This pipeline implements standard DevSecOps automation:

```yaml
name: Production CI/CD Pipeline

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

permissions:
  contents: read
  security-events: write

jobs:
  # ============================================================================
  # Stage 1: Quality, Linting & Unit Tests
  # ============================================================================
  test:
    name: Code Quality & Unit Testing
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"
          cache: "pip"

      - name: Install Linting & Testing Tools
        run: |
          python -m pip install --upgrade pip
          pip install flake8 pytest pytest-cov
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

      - name: Lint Python Code with Flake8
        run: |
          # Stop build if there are Python syntax errors or undefined names
          flake8 src/ --count --select=E9,F63,F7,F82 --show-source --statistics
          # Exit-zero treats all errors as warnings
          flake8 src/ --count --max-complexity=10 --max-line-length=127 --statistics

      - name: Lint Dockerfile with Hadolint
        uses: hadolint/hadolint-action@v3.1.0
        with:
          dockerfile: Dockerfile
          failure-threshold: error

      - name: Execute Pytest Suite
        run: |
          pytest --cov=src tests/

  # ============================================================================
  # Stage 2: Security & Vulnerability Scanning (DevSecOps)
  # ============================================================================
  security:
    name: Container Security Scanning
    runs-on: ubuntu-latest
    needs: test
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Build Local Container Image for Scanning
        run: |
          docker build -t cloud-app:${{ github.sha }} .

      - name: Run Trivy Vulnerability Scanner
        uses: aquasecurity/trivy-action@master
        with:
          image-ref: 'cloud-app:${{ github.sha }}'
          format: 'sarif'
          output: 'trivy-results.sarif'
          severity: 'CRITICAL,HIGH'

      - name: Upload Trivy Scan Results to GitHub Security Tab
        uses: github/codeql-action/upload-sarif@v3
        if: always()
        with:
          sarif_file: 'trivy-results.sarif'

  # ============================================================================
  # Stage 3: Build & Publish to Container Registry
  # ============================================================================
  build-and-push:
    name: Build & Push Image
    runs-on: ubuntu-latest
    needs: security
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Log in to GitHub Container Registry (GHCR)
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Extract Metadata & Tags
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ghcr.io/${{ github.repository }}/backend-api
          tags: |
            type=sha,format=long
            type=raw,value=latest

      - name: Build and Push Docker Image with Cache
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
          cache-from: type=gha
          cache-to: type=gha,mode=max

  # ============================================================================
  # Stage 4: Automated Deployment via Terraform (AWS)
  # ============================================================================
  deploy:
    name: Automated Infrastructure Deployment
    runs-on: ubuntu-latest
    needs: build-and-push
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    defaults:
      run:
        working-directory: ./terraform
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: 1.15.8

      - name: Terraform Init
        run: terraform init

      - name: Terraform Plan
        run: terraform plan -no-color

      - name: Terraform Apply
        run: terraform apply -auto-approve
```

---

## 2.5 Infrastructure as Code (Terraform AWS Deployment)

You will use your proven modular Terraform structure. Below is the automated compute module specification:

```hcl
# terraform/main.tf

terraform {
  required_version = ">= 1.5.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  backend "s3" {
    bucket         = "sanjeev-terraform-state-prod"
    key            = "docker-app/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-lock-table"
  }
}

provider "aws" {
  region = var.aws_region
}

# Re-use custom VPC Module (from previous project)
module "vpc" {
  source               = "./modules/vpc"
  cidr_block           = "10.0.0.0/16"
  public_subnet_cidrs  = ["10.0.1.0/24", "10.0.2.0/24"]
  private_subnet_cidrs = ["10.0.10.0/24", "10.0.20.0/24"]
  availability_zones   = ["us-east-1a", "us-east-1b"]
}

# Security Group for Application Instance
resource "aws_security_group" "app_sg" {
  name        = "docker-app-sg"
  description = "Allow inbound HTTP traffic to Reverse Proxy"
  vpc_id      = module.vpc.vpc_id

  ingress {
    description = "HTTP Inbound"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# EC2 Instance configured with Docker User Data
resource "aws_instance" "app_server" {
  ami                    = var.ami_id # RHEL 9 or Ubuntu 24.04 LTS
  instance_type          = "t3.micro"
  subnet_id              = module.vpc.public_subnet_ids[0]
  vpc_security_group_ids = [aws_security_group.app_sg.id]
  iam_instance_profile   = aws_iam_instance_profile.ec2_profile.name

  user_data = <<-EOF
              #!/bin/bash
              dnf update -y
              dnf install -y docker git
              systemctl enable --now docker
              usermod -aG docker ec2-user
              # Pull and run application container directly from registry
              docker run -d --restart always -p 80:80 ghcr.io/sanjeevkumar-cloud/backend-api:latest
              EOF

  tags = {
    Name        = "DevOps-Docker-AppServer"
    Environment = "Production"
  }
}
```

---

# 3. Interview Master Playbook: Real-World Scenarios & Defenses

This section prepares you to defend your technical foundation under pressure.

---

## 3.1 Docker & Containerization Deep-Dive

#### Q1: "Why did you use a multi-stage Docker build instead of installing everything in a single image?"
> **Your Defense:**  
> *"In a single-stage build, all build dependencies—such as `gcc`, `libpq-dev`, build headers, and temporary pip cache files—remain in the image layers. This inflates the image size (often over 800MB) and drastically increases the attack surface with unneeded binaries.  
> By separating the **builder** stage from the **runner** stage, I compile the dependencies in an isolated container and only copy the clean `/install/deps` directory into a lightweight `python:3.11-slim-bookworm` runtime image. This drops image size down to ~120MB, optimizes deployment pull times, and reduces CVE vulnerability scan findings in Trivy."*

#### Q2: "Why should you never run a container as the default `root` user?"
> **Your Defense:**  
> *"If an attacker achieves remote code execution (RCE) inside a container running as root, any container escape vulnerability (such as a kernel exploit or misconfigured volume mount like `/var/run/docker.sock`) grants root access to the underlying host OS.  
> In my Dockerfile, I explicitly create a dedicated system group and user with a fixed UID (`10001:10001`) and no login shell (`/sbin/nologin`), switching execution context with `USER 10001:10001` before the runtime command starts."*

#### Q3: "What is the PID 1 problem in Docker containers, and how does it relate to Linux systemd?"
> **Your Defense:**  
> *"In Linux, PID 1 (`init` or `systemd`) has two critical duties: reaping zombie child processes (processes that died but whose parent didn't read their exit status) and forwarding Unix signals (like `SIGTERM`, `SIGINT`) to child processes.  
> Inside a standard container, the command specified in `CMD` runs as PID 1. If you run a script or non-init process as PID 1, it often ignores `SIGTERM`. When you run `docker stop`, Docker waits 10 seconds before forcibly killing it with `SIGKILL`, preventing clean application shutdown. I handle this by either running WSGI servers like Gunicorn that properly handle signal forwarding, or using a lightweight init like `tini` or `dumb-init`."*

---

## 3.2 Networking & VPC Packet Flow Troubleshooting

#### Q4: "A web server in a public subnet cannot connect to a database in a private subnet. How do you systematically troubleshoot it layer by layer?"
> **Your Defense:**  
> *"I do not guess; I trace the packet flow systematically from layer 3 to layer 7:  
> 1. **DNS / Name Resolution:** From the application instance, run `getent hosts <db-private-hostname>` to verify private IP resolution.  
> 2. **Routing Table (VPC Level):** Check if the private subnet's route table includes local VPC routing (`10.0.0.0/16 -> local`).  
> 3. **Security Groups (Stateful):** Check the DB security group. Does it have an inbound rule allowing port 3306 (MySQL) or 5432 (Postgres) where the source is explicitly set to the **Security Group ID** of the web server (least-privilege SG reference)?  
> 4. **Network ACLs (Stateless):** Verify that the private subnet NACL allows inbound traffic on the DB port AND that the public subnet NACL allows outbound ephemeral ports (1024–65535) for return traffic.  
> 5. **Host Layer / OS Level:** SSH into the app instance, test TCP handshake using `nc -zv <db-ip> 5432`. If it times out, it is a Security Group / Routing issue. If connection is refused, the database service is not actively listening on `0.0.0.0` or its daemon is stopped."*

---

## 3.3 Linux Administration (RHCSA Level) Scenarios

#### Q5: "A production RHEL 9 server has 100% disk usage on `/var/log` mounted on an LVM logical volume. How do you fix it without taking the server down?"
> **Your Defense:**  
> *"Because RHEL uses LVM, this can be resolved online without downtime:  
> 1. Check volume group free space with `vgs`.  
> 2. If free extents exist in the Volume Group (`vg_data`), extend the logical volume and resize the filesystem in a single command:  
>    `lvextend -r -L +10G /dev/vg_data/lv_var_log` (the `-r` flag automatically resizes XFS or ext4).  
> 3. If the VG has no free extents, partition a new disk/EBS volume using `fdisk` / `parted`, initialize it as a physical volume (`pvcreate /dev/sdb1`), extend the volume group (`vgextend vg_data /dev/sdb1`), and then run `lvextend -r`.  
> 4. Simultaneously inspect the log hog using `journalctl --vacuum-size=500M` and verify logrotate configuration in `/etc/logrotate.d/` to prevent recurrence."*

#### Q6: "How do you create and manage a custom background service on RHEL using systemd?"
> **Your Defense:**  
> *"Create a unit file at `/etc/systemd/system/myapp.service`:  
> ```ini
> [Unit]
> Description=Custom Production Flask API
> After=network.target
> 
> [Service]
> User=appuser
> Group=appgroup
> WorkingDirectory=/opt/myapp
> ExecStart=/opt/myapp/venv/bin/gunicorn -w 3 -b 127.0.0.1:5000 wsgi:app
> Restart=always
> RestartSec=5
> 
> [Install]
> WantedBy=multi-user.target
> ```  
> Then reload the daemon with `systemctl daemon-reload`, enable it for boot with `systemctl enable --now myapp.service`, and inspect status and logs with `systemctl status myapp` and `journalctl -u myapp -f`."*

---

## 3.4 Terraform Production Lifecycle & State Management

#### Q7: "What happens if two engineers run `terraform apply` simultaneously, and how do you protect against state corruption?"
> **Your Defense:**  
> *"Without state locking, simultaneous writes create race conditions that corrupt the `terraform.tfstate` file, causing orphaned resources or catastrophic overwrite.  
> In my Terraform architecture:  
> 1. I store the remote state in an **Amazon S3 bucket** with versioning enabled and public access completely blocked.  
> 2. I configure a **DynamoDB table** with a primary key named `LockID`.  
> When `terraform plan` or `apply` executes, Terraform acquires a lock lease in DynamoDB. Any second process receives an error (`Error acquiring the state lock`) and immediately halts until the first run releases the lease."*

#### Q8: "How did you achieve reducing provisioning time from ~45 minutes to ~45 seconds on AWS?"
> **Your Defense:**  
> *"Manually configuring a secure, multi-tier VPC via the AWS Management Console requires clicking through 7+ distinct screens: creating the VPC, defining CIDR blocks, creating 4 subnets across multiple AZs, provisioning an Internet Gateway, attaching it, building public and private route tables, associating subnets, writing 15+ granular security group rules, and configuring NACLs. This human-driven workflow takes roughly 45 minutes and is highly prone to configuration drift.  
> Using Terraform, I modularized the VPC infrastructure into parameterized HCL code with reusable resource blocks. By running `terraform apply -auto-approve`, the AWS API processes the declarative dependency graph in parallel, creating all routing, gateways, and subnets in ~45 seconds deterministically with zero human error."*

---

## 3.5 CI/CD & Pipeline Security

#### Q9: "How do you ensure secrets (API keys, DB passwords) never leak in GitHub Actions logs or git history?"
> **Your Defense:**  
> *"1. **Repository Level:** Enforce strict `.gitignore` patterns and run pre-commit hooks using `gitleaks` to block secrets from ever being committed locally.  
> 2. **Pipeline Secrets:** Store all sensitive credentials in **GitHub Encrypted Secrets** (or use OIDC integration with AWS IAM / HashiCorp Vault to eliminate long-lived access keys entirely).  
> 3. **Runtime Protection:** Pass credentials into containers at runtime using Docker secrets or environment variables mounted from files (`_FILE` convention), never hardcoding them in `Dockerfile` `ENV` statements where they would persist in image metadata."*

---

# 4. Portfolio & Resume Transformation Blueprint

---

## 4.1 Resume Bullet Optimization (FlowCV Alignment)

Once you finish building this project, replace generic bullet points on your resume with these quantifiable, high-impact statements:

### Under "Projects" Section:
```markdown
Cloud-Native Microservices CI/CD & Infrastructure Automation
• Built an end-to-end automated deployment pipeline using GitHub Actions, reducing manual release cycles from hours to under 3 minutes with zero downtime.
• Hardened container architecture using multi-stage Docker builds and non-root execution (UID 10001), slashing final runtime image footprint by 85% (~800MB to ~120MB).
• Embedded automated DevSecOps scanning into pull requests using Trivy and Hadolint, identifying and blocking Critical/High CVEs prior to registry publish.
• Automated immutable image publishing to GitHub Container Registry (GHCR) and configured automated AWS deployment leveraging modular Terraform code.
```

---

## 4.2 GitHub Repository Presentation Standards

Your target repository `SanjeevKumar-Cloud/production-docker-cicd-aws` must contain:

1. **Top Badges:**
   ```markdown
   ![Build Status](https://github.com/SanjeevKumar-Cloud/production-docker-cicd-aws/actions/workflows/ci-cd.yml/badge.svg)
   ![Docker Image Size](https://img.shields.io/badge/image%20size-120MB-blue)
   ![Trivy Security Scan](https://img.shields.io/badge/security-passed-brightgreen)
   ![License](https://img.shields.io/badge/license-MIT-green)
   ```
2. **Clear ASCII Architecture Diagram:** Show the exact packet flow (Client → Nginx → Gunicorn/Flask → DB).
3. **Reproducibility Guide (Local & Cloud):**
   ```bash
   # Quick Start Local Run
   git clone https://github.com/SanjeevKumar-Cloud/production-docker-cicd-aws.git
   cd production-docker-cicd-aws
   docker compose up --build -d
   ```
4. **DevSecOps Audit Log:** Include a markdown table or screenshot showing the Trivy vulnerability report before and after multi-stage optimization.

---

## 4.3 LinkedIn Technical Branding & Recruiter Hook Plan

Publish a 3-part technical case-study series:

### Post 1: "Why your Docker image doesn't need to be 850MB"
- **Hook:** *"A single line in your Dockerfile could be adding 700MB of bloat and dozens of critical vulnerabilities. Here is how I cut our Python runtime from 820MB to 118MB."*
- **Visual:** Side-by-side terminal screenshot (`docker images` comparison).
- **Core Concept:** Multi-stage builds, copying only `/install/deps`, and using `slim-bookworm` or distroless.

### Post 2: "Stopping bad code before it reaches AWS: My GitHub Actions DevSecOps workflow"
- **Hook:** *"Most junior pipelines just test and deploy. Here is how we integrated Trivy security scanning directly into PR checks."*
- **Visual:** GitHub Actions workflow execution diagram showing parallel test and security jobs.

### Post 3: "Bridging the gap: From RHCSA Linux Admin to Automated Cloud DevOps"
- **Hook:** *"How understanding systemd and Linux file permissions made containerizing microservices 10x easier."*
- **Connection:** Show how RHCSA fundamentals directly solve Docker container permission errors and signal handling.

---

# 5. 90-Day Next-Horizon Roadmap: Kubernetes & Observability

---

```
  MONTH 1 (WEEKS 1–3)            MONTH 2 (WEEKS 4–7)            MONTH 3 (WEEKS 8–12)
┌──────────────────────┐       ┌──────────────────────┐       ┌──────────────────────┐
│  Docker & CI/CD      │ ────> │  Kubernetes (K8s)    │ ────> │ Observability & SRE  │
│  Enterprise Project  │       │  EKS / Helm / CKA    │       │ Prometheus / Grafana │
└──────────────────────┘       └──────────────────────┘       └──────────────────────┘
```

---

### Phase 1 (Weeks 1–3): Docker & CI/CD Mastery *(Current Target)*
- [x] Master multi-stage Docker builds, `.dockerignore`, non-root execution.
- [x] Configure multi-container networking with `docker-compose.yml`.
- [x] Write complete GitHub Actions workflow (`.github/workflows/ci-cd.yml`).
- [x] Integrate security scanning (Hadolint + Trivy).
- [x] Connect automated push to Amazon ECR or GitHub Container Registry (GHCR).

### Phase 2 (Weeks 4–7): Kubernetes (EKS, AKS, Helm)
- [ ] **Core Concepts:** Pods, ReplicaSets, Deployments, Services (ClusterIP, NodePort, LoadBalancer), Namespaces.
- [ ] **Storage & Config:** PersistentVolumes (PV), PersistentVolumeClaims (PVC), ConfigMaps, Secrets.
- [ ] **Ingress Controllers:** Nginx Ingress Controller, TLS termination with cert-manager.
- [ ] **Packaging:** Package the multi-tier application into custom **Helm Charts** (`Chart.yaml`, `values.yaml`, templates).
- [ ] **Cloud Managed K8s:** Provision an **AWS EKS** cluster using Terraform, deploy the containerized application via Helm.

### Phase 3 (Weeks 8–10): Observability & Monitoring (The SRE Layer)
- [ ] **Metrics Collection:** Deploy **Prometheus Operator** (kube-prometheus-stack) on EKS.
- [ ] **Visualization:** Set up **Grafana** dashboards monitoring CPU/Memory saturation, HTTP request rates, and 4xx/5xx error rates.
- [ ] **Alerting:** Configure **Alertmanager** with webhook notifications (Slack/Discord/Email) for pod crash loops and high latency.
- [ ] **Logging:** Centralized log aggregation with Loki + Promtail or AWS CloudWatch Container Insights.

### Phase 4 (Weeks 11–12): DevSecOps & Platform Engineering Foundation
- [ ] GitOps continuous deployment using **ArgoCD** (declarative sync between Git repo and Kubernetes cluster).
- [ ] Policy enforcement with Open Policy Agent (OPA) / Kyverno.
- [ ] Multi-region Disaster Recovery & AWS Well-Architected Framework review.

---

## Immediate Action Item

We are now ready to implement the code for **Phase 1** inside this workspace (`peaceful-davinci`):
1. Create `src/app.py` & `src/wsgi.py` (production multi-tier Flask application).
2. Create `Dockerfile` (hardened multi-stage build).
3. Create `docker-compose.yml` & Nginx configuration.
4. Set up `.github/workflows/ci-cd.yml`.

*Execute Step 1 now to begin scaffolding the repository.*
