---
title: "Week 1 Worklog"
date: 2026-06-22
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

* Initialize the AWS environment & establish basic infrastructure security for the game project.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| Mon | - Enable Multi-Factor Authentication (MFA) for the AWS Root account.<br>- Setup users and assign IAM permissions using the Least Privilege principle for Developers. | 06/22/2026 | 06/22/2026 |
| Tue | - Learn about and initialize an Amazon S3 Bucket.<br>- Configure access permissions and CORS policies for S3. | 06/23/2026 | 06/23/2026 |
| Wed | - Upload initial Game assets to S3: UI images, character sprites, weapons, and configuration files (JSON). | 06/24/2026 | 06/24/2026 |
| Thu | - Design basic network architecture: Create a VPC, setup Public/Private Subnets. | 06/25/2026 | 06/25/2026 |
| Fri | - Configure Security Groups to secure access flows.<br>- Launch an EC2 instance and test secure SSH/RDP connections. | 06/26/2026 | 06/27/2026 |

### Week 1 Achievements:

During the first week, I successfully set up the foundational AWS environment and ensured security standards for the project:

* **Account Security:** Successfully enabled MFA for the Root account to prevent unauthorized access. Created an IAM Group and granted Least Privilege permissions for developer roles, securing interactions with AWS.
* **Asset Storage (S3):** Successfully initialized an S3 Bucket to centrally store all game assets such as UI images and character/weapon sprites. This allows the Unity game to easily fetch data via URLs without packing them directly into the build, reducing the application size.
  
  ![S3 Bucket Structure for Assets](/images/week1/s3_bucket.png)
  *(Note: Need to add S3 Bucket image here)*

* **Network Infrastructure (VPC & EC2):** Established a dedicated VPC for the game environment, including Subnets and tightly controlled Security Groups. Launched a test EC2 instance and successfully made a secure SSH connection, paving the way for more complex backend setups in upcoming weeks.
