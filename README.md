# ☁️ Cloud Portfolio | Cloud Engineering & DevOps

<p align="center">
  <img src="https://img.shields.io/badge/AWS-Cloud%20Computing-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="AWS Cloud Computing" />
  <img src="https://img.shields.io/badge/Focus-Cloud%20%26%20DevOps-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Cloud and DevOps" />
  <img src="https://img.shields.io/badge/Status-Always%20Learning-22C55E?style=for-the-badge" alt="Always Learning" />
</p>

<p align="center">
  <strong>Building, breaking, understanding, and improving cloud infrastructure.</strong>
  <br />
  A hands-on portfolio documenting my journey in Cloud Computing, AWS, Infrastructure, Security, Automation, and DevOps.
</p>

---

## 👨‍💻 About This Portfolio

Welcome! This repository is where I document my practical experience, technical experiments, and continuous learning in cloud technologies.

My approach goes beyond simply completing labs. I aim to understand **how each component works, why architectural decisions matter, and how to build infrastructure that is scalable, secure, resilient, and cost-efficient.**

Here, you'll find practical implementations, architecture diagrams, technical documentation, troubleshooting notes, scripts, and evidence of the results obtained.

### 🎯 What I'm Working Towards

- ☁️ **Cloud Engineering:** Building and understanding cloud infrastructure using AWS.
- ⚙️ **DevOps & Automation:** Exploring infrastructure as code, scripting, containers, and deployment workflows.
- 🔐 **Cloud Security:** Learning identity management, permissions, network security, and security best practices.
- 📈 **Reliability & Monitoring:** Understanding availability, scalability, observability, and performance.
- 🌍 **Continuous Growth:** Developing the technical and English communication skills needed to work in international technology teams.

---

## 🧭 Explore the Portfolio

| Area | What You'll Find |
|---|---|
| ☁️ AWS Infrastructure | EC2, VPC, networking, load balancing, and Auto Scaling |
| 🔐 Security & IAM | Identity, permissions, access control, and security configurations |
| 📊 Monitoring | CloudWatch metrics, alarms, health checks, and troubleshooting |
| ⚙️ Automation | AWS CLI, scripts, Infrastructure as Code, and repeatable deployments |
| 🐧 Systems & Networking | Linux, network fundamentals, connectivity, and diagnostics |
| 📚 Documentation | Architecture diagrams, implementation guides, technical decisions, and lessons learned |

---

## ⭐ Featured Project

### 01. AWS Load Balancing & Auto Scaling

**Designing a scalable and highly available web application architecture.**

> Objective: Distribute incoming HTTP traffic across multiple EC2 instances and automatically adjust infrastructure capacity in response to workload changes.

**Architecture overview**

The solution uses an Application Load Balancer in public subnets to distribute incoming traffic to EC2 instances running in private subnets across two Availability Zones.

An EC2 Auto Scaling group manages the instances, while Amazon CloudWatch monitors CPU utilization and supports automatic scaling decisions.

**Key components**

- **Application Load Balancer (ALB):** Distributes incoming application traffic.
- **Amazon EC2:** Runs the web application instances.
- **EC2 Auto Scaling:** Maintains capacity and scales the instance fleet.
- **Launch Templates & AMIs:** Standardize instance configuration.
- **Amazon CloudWatch:** Monitors metrics and scaling alarms.
- **Amazon VPC:** Provides network isolation through public and private subnets.

**Scaling configuration**

| Setting | Configuration |
|---|---|
| Minimum capacity | 2 instances |
| Desired capacity | 2 instances |
| Maximum capacity | 4 instances |
| Scaling metric | Average CPU utilization |
| Target utilization | 50% |
| Availability | 2 Availability Zones |

**What I practiced**

- Creating a reusable Amazon Machine Image.
- Configuring an Application Load Balancer and target group.
- Deploying EC2 instances through a Launch Template.
- Configuring an Auto Scaling group across private subnets.
- Validating target health and application access.
- Triggering additional capacity through load testing.
- Monitoring infrastructure behavior through CloudWatch alarms.

**Evidence & Documentation**

- [ ] Architecture diagram
- [ ] Load balancer and target group screenshots
- [ ] Auto Scaling configuration and instance screenshots
- [ ] CloudWatch alarm and scaling test evidence
- [ ] Implementation notes and lessons learned

Project status: **Lab completed; documentation and evidence are being organized.**

*This project was implemented in a learning environment. The infrastructure is not necessarily running continuously.*

---

## 🛠️ Technologies & Tools

### Cloud

<p>
  <img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=FF9900" alt="AWS" />
  <img src="https://img.shields.io/badge/EC2-FF9900?style=flat-square&logo=amazonec2&logoColor=white" alt="Amazon EC2" />
  <img src="https://img.shields.io/badge/VPC-8C4FFF?style=flat-square&logo=amazonaws&logoColor=white" alt="Amazon VPC" />
  <img src="https://img.shields.io/badge/CloudWatch-FF4F8B?style=flat-square&logo=amazonaws&logoColor=white" alt="Amazon CloudWatch" />
  <img src="https://img.shields.io/badge/IAM-232F3E?style=flat-square&logo=amazonaws&logoColor=white" alt="AWS IAM" />
</p>

### Systems, Networking & Automation

<p>
  <img src="https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black" alt="Linux" />
  <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" alt="Git" />
  <img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub" />
  <img src="https://img.shields.io/badge/AWS_CLI-232F3E?style=flat-square&logo=amazonaws&logoColor=white" alt="AWS CLI" />
</p>

*This section reflects the technologies represented in my current learning and project documentation. Additional tools will be added as I gain practical experience with them.*

---

## 📂 Repository Structure

```text
cloud-portfolio/
├── README.md
│
├── aws/
│   ├── load-balancing-autoscaling/
│   │   ├── README.md
│   │   ├── architecture/
│   │   ├── screenshots/
│   │   └── scripts/
│   │
│   ├── networking/
│   └── security-iam/
│
├── linux/
│   └── monitoring/
│
└── projects/
```

*The structure will evolve as new projects, experiments, and documentation are added.*

---

## 🧠 My Approach to Learning

I believe technical growth comes from understanding, not just execution.

For each project, I aim to document:

- **The problem:** What am I trying to solve?
- **The architecture:** Which components are involved, and why?
- **The implementation:** How was the solution configured?
- **The validation:** How did I verify that it worked?
- **The troubleshooting:** What failed, and how did I investigate it?
- **The improvement:** What would I change for a production environment?

My goal is to turn practical exercises into reusable technical knowledge and progressively build more independent, real-world projects.

---

## 🚀 What's Next?

My learning roadmap includes:

- [ ] Expand AWS networking and security projects.
- [ ] Practice AWS CLI and infrastructure automation.
- [ ] Build infrastructure using Terraform.
- [ ] Containerize an application using Docker.
- [ ] Explore CI/CD pipelines and deployment automation.
- [ ] Improve monitoring, logging, and incident troubleshooting.
- [ ] Develop more complete end-to-end cloud projects.

This roadmap will evolve as I progress and identify new areas to explore.

---

## 🤝 Let's Connect

I'm always interested in learning from other professionals, exchanging ideas, and discussing cloud architecture, infrastructure, and DevOps.

- 💼 **LinkedIn:** [Connect with me](www.linkedin.com/in/enzo-rodrigoo)
- 🐙 **GitHub:** Explore my repositories and follow my progress.

---

<p align="center">
  <strong>Build. Learn. Improve. Repeat.</strong>
  <br />
  <em>Every project is an opportunity to understand technology a little better.</em>
  <br /><br />
  ⭐ Thanks for visiting my portfolio!
</p>
