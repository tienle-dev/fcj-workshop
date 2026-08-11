---
title: "Week 5 Worklog"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Build a Serverless Backend architecture (AWS Lambda & API Gateway) for the game.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| Mon | - Refactor the .NET 8 Backend source code to fit the Serverless architecture.<br>- Create independent AWS Lambda Handlers. | 07/20/2026 | 07/20/2026 |
| Tue | - Separate processing logic into distinct functional clusters: Auth, Character, Inventory, Story, Battle. | 07/21/2026 | 07/21/2026 |
| Wed | - Configure Amazon API Gateway to create RESTful API Endpoints.<br>- Link API Gateway with corresponding AWS Lambda functions. | 07/22/2026 | 07/22/2026 |
| Thu | - Use `dotnet publish` to compile C# code into a standard .NET 8 build.<br>- Configure appropriate Memory (RAM) and Timeout settings for different Lambda functions. | 07/23/2026 | 07/23/2026 |
| Fri | - Deploy and test the complete Serverless system.<br>- Update the new endpoint URL in the Unity source code and test the game flow. | 07/24/2026 | 07/25/2026 |

### Week 5 Achievements:

This week marked a major transformation for the system as I completely migrated the traditional Backend architecture to a modern Serverless model on AWS:

* **Completion of AWS Lambda Handlers:** All business logic (Auth, Character, Inventory, Story, Battle) was broken down into separate Lambda functions running on .NET 8. This breakdown makes the application easy to maintain, and each function can automatically scale independently based on the number of players.
* **API Gateway Integration:** Successfully established the API Gateway communication portal connecting directly to the Lambda functions. This gateway acts as a "receptionist", receiving all RESTful API requests from the client (Unity game), validating them, and forwarding them to the correct handler function.
* **AWS Lambda Configuration Optimization:** Instead of using complex and bulky Docker setups, I directly built the .NET 8 code (using `dotnet publish`) and pushed it to Lambda. I also fine-tuned the settings: standard API functions are allocated 512MB of RAM, while functions interacting with Bedrock AI are granted 1024MB to ensure the fastest possible response times.

