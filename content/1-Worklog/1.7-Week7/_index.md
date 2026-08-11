---
title: "Week 7 Worklog"
date: 2026-08-03
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Security, Monitoring & Operational Cost Optimization for the AWS system.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| Mon | - Review Backend code to remove sensitive configuration info from the source code.<br>- Use Environment Variables for Lambda functions. | 08/03/2026 | 08/03/2026 |
| Tue | - Verify IAM Roles to ensure Lambda connects to DynamoDB and Bedrock securely. | 08/04/2026 | 08/04/2026 |
| Wed | - Use CloudWatch to create a Dashboard (`RPG-Game-Backend`) for tracking key system metrics. | 08/05/2026 | 08/05/2026 |
| Thu | - Set up automated Alarms to send notifications if Lambda functions encounter too many errors. | 08/06/2026 | 08/06/2026 |
| Fri | - Check AWS Cost Explorer to review costs.<br>- Clean up unused resources (old Snapshots, etc.) to save money. | 08/07/2026 | 08/08/2026 |

### Week 7 Achievements:

With the system basically complete, I dedicated this week to ensuring the game runs not only smoothly but also securely and cost-effectively:

* **Security & Configuration:** Instead of hardcoding sensitive information, I switched to using Environment Variables for Lambda. Connections to the Database (DynamoDB) and AI (Bedrock) are also secured via IAM Roles, keeping the code pushed to GitHub much safer and cleaner.
* **System Monitoring with CloudWatch:** I created a Dashboard named `RPG-Game-Backend` on CloudWatch to easily monitor the game's status. I also added Alarms to automatically trigger alerts whenever the game logic Lambda functions fail, making future debugging much faster.
* **Cost Optimization:** Spent time reviewing cost charts on AWS Cost Explorer to delete unused background resources, preventing unnecessary charges during operation.

  ![CloudWatch Monitoring Dashboard1](../../../images/1-Worklog/1.7-Week7/bedrock-cloudwatch.png)
  ![CloudWatch Monitoring Dashboard2](../../../images/1-Worklog/1.7-Week7/lambda-cloudwatch.png)
  *CloudWatch Monitoring Dashboard*
