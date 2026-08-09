---
title: "Week 6 Worklog"
date: 2026-07-27
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Cloud Infrastructure Automation (Infrastructure as Code - AWS CDK).

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| Mon | - Learn about the concept of Infrastructure as Code (IaC) and the AWS CDK tool.<br>- Initialize a CDK project using C#. | 07/27/2026 | 07/27/2026 |
| Tue | - Write source code defining CognitoStack (User Pool, App Client) and DatabaseStack (DynamoDB). | 07/28/2026 | 07/28/2026 |
| Wed | - Write source code defining LambdaStack (handler functions) and ApiStack (API Gateway). | 07/29/2026 | 07/29/2026 |
| Thu | - Configure the CI/CD pipeline using GitHub Actions.<br>- Automate building Docker Images and deploying infrastructure directly from the GitHub repository. | 07/30/2026 | 07/30/2026 |
| Fri | - Practice running CDK CLI commands (`cdk synth`, `cdk deploy`, `cdk destroy`).<br>- Evaluate flexibility in resource management. | 07/31/2026 | 08/01/2026 |

### Week 6 Achievements:

Instead of manually configuring each service on the AWS web interface (Console), this week I applied the Infrastructure as Code (IaC) methodology using the AWS Cloud Development Kit (CDK) to fully automate the deployment process:

* **Writing Infrastructure in C# Code:** I used the familiar C# language to program the Stacks that define the entire system, including: CognitoStack, DatabaseStack, LambdaStack, and ApiStack. Coding the infrastructure helps me easily manage versions (version control) and avoid errors caused by manual configuration.
* **CI/CD Integration with GitHub Actions:** Successfully set up the CI/CD pipeline. Now, whenever code changes are pushed to the main branch of the GitHub repository, the system automatically builds the Docker image and triggers the AWS CDK deploy command to update the infrastructure without manual intervention.
* **Flexible Resource Management:** Mastered the use of CDK CLI commands. As a result, I can spin up a complete copy of the entire system (deploy) in just a few minutes, and completely tear it down (destroy) safely when no longer needed, optimizing costs.

  ![GitHub Actions CI/CD Interface](/images/week6/github_actions.png)
  *(Note: Need to add a screenshot of a successful GitHub Actions run here)*

  ```csharp
  // Example code snippet defining LambdaStack using AWS CDK C#
  ```
  *(Note: Insert an illustrative C# CDK code snippet here)*
