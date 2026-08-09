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
| Mon | - Review the entire Backend source code to remove hardcoded connection strings.<br>- Configure secret key storage on AWS Secrets Manager. | 08/03/2026 | 08/03/2026 |
| Tue | - Integrate the Backend to call and decrypt connection strings from Secrets Manager at runtime. | 08/04/2026 | 08/04/2026 |
| Wed | - Set up Amazon CloudWatch, create a system monitoring Dashboard.<br>- Push key metrics to the Dashboard: API Gateway latency, number of Lambda invocations. | 08/05/2026 | 08/05/2026 |
| Thu | - Monitor and set up Alarms for Amazon Bedrock API usage costs. | 08/06/2026 | 08/06/2026 |
| Fri | - Use AWS Cost Explorer to review system-wide resources.<br>- Perform cleanup of orphaned resources (unused EBS, Elastic IPs) to optimize AWS usage costs. | 08/07/2026 | 08/08/2026 |

### Week 7 Achievements:

With the system basically complete, I dedicated this week to ensuring the game runs not only smoothly but also securely and cost-effectively:

* **Security with AWS Secrets Manager:** Completely eliminated the risk of sensitive information leakage. All Database connection strings and Bedrock API keys were moved to secure encrypted storage on AWS Secrets Manager. Lambda functions only retrieve the keys at runtime, ensuring the source code (pushed to GitHub) is completely clean.
* **Visual Monitoring with CloudWatch:** Successfully built an overview Dashboard on Amazon CloudWatch. From here, I can monitor system "health" in real-time, such as API Gateway latency, Lambda invocation frequency, or quickly detect error rates.
* **Operational Cost Optimization:** Used AWS Cost Explorer to analyze cost charts. Through this, I detected and cleaned up "forgotten" resources (like old EBS snapshots, unattached Elastic IPs) and limited the budget to prevent unexpected bills from the AI API.

  ![CloudWatch Monitoring Dashboard](/images/week7/cloudwatch_dashboard.png)
  *(Note: Need to add a screenshot of the CloudWatch Dashboard here)*
