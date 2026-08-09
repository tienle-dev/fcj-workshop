---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Project Proposal: AI Dungeon RPG Adventure Game

## 1. Executive Summary

The **AI Dungeon RPG Adventure Game** represents a significant leap forward in the Role-Playing Game (RPG) genre. This project merges the limitless creativity of Generative Artificial Intelligence with the highly scalable, cost-efficient AWS Serverless architecture.

The game allows players to create characters and embark on completely open-ended adventures. Storylines, challenges, and Turn-based Boss battles are not pre-programmed; rather, they are dynamically generated in real-time based on the player's choices using **AWS Bedrock**. This immersive experience is presented through a vibrant **Unity 2D Client** connected to a robust **.NET 8 Backend** on AWS.

## 2. Problem Statement

### The Pitfalls of Traditional RPGs
*   **Rigid Storylines:** Traditional RPGs are bound by hard-coded, branching scripts. Regardless of the development effort, content eventually runs out, leading to repetition and drastically reducing replayability.
*   **Massive Overhead Costs:** Running traditional, stateful game servers involves substantial costs for idle hardware and poses a massive logistical challenge when scaling to accommodate sudden player surges.

### The Breakthrough Solution
*   **Dynamic AI Storytelling:** By integrating Large Language Models (LLMs) via **AWS Bedrock**, the game generates environments, scenarios, and contextually accurate consequences on the fly based on player inputs.
*   **Flexible Serverless Infrastructure:** Core game mechanics (authentication, inventory, battle logic) are executed via **AWS Lambda** and data is persisted in **Amazon DynamoDB**. This allows the game to automatically scale with player traffic while adopting a highly economical Pay-as-you-go model.

## 3. Solution Architecture

The project employs a 100% Serverless architecture on AWS, strictly separating the Game Client from the Cloud Backend to ensure security and performance.

![AWS Architecture Diagram](images/aws-architect-project.png)
*(System Architecture Overview)*

*   **Amazon API Gateway & Cognito:** Serves as the secure entry point, managing player authentication (Login/Register) and validating JWT Tokens for all incoming requests.
*   **Compute Tier (AWS Lambda - .NET 8):** Distributed functions handle the heavy lifting: managing character states, resolving turn-based combat, handling inventory logic, and interfacing with the AI models.
*   **Database Tier (Amazon DynamoDB):** A low-latency NoSQL database that persistently stores character stats, game items, and ongoing story sessions.
*   **AWS Bedrock:** The creative "brain" of the game that processes the game's context to generate real-time storytelling.

## 4. Technical Implementation

The project adopts a **Monorepo** design pattern, enabling direct sharing of C# Domain Models and Data Transfer Objects (DTOs) between the Unity Client and the Lambda Backend.
*   **Frontend (Game Client):** Developed in Unity (C#) utilizing the 2D Universal Render Pipeline (URP). It communicates with the backend exclusively via RESTful APIs.
*   **Backend & Infrastructure as Code (IaC):** The entire AWS infrastructure is defined using the **AWS CDK (C#)**, ensuring rapid, consistent, and error-free deployments across multiple environments.
*   **Security:** Implements a strict Server-Authoritative architecture. All critical calculations (health points, damage outputs, loot drops) are processed securely inside AWS Lambda, effectively neutralizing client-side cheating or hacking attempts.

## 5. Timeline & Milestones

*   **Milestone 1 (22/06/2026 - 05/07/2026):** Finalize the core architecture, initialize AWS CDK, and successfully deploy Amazon Cognito (Auth) alongside the DynamoDB schemas.
*   **Milestone 2 (06/07/2026 - 19/07/2026):** Integrate AWS Bedrock by developing context-aware `Prompt Builders` and a robust JSON `Response Parser` to translate AI text into actionable game data.
*   **Milestone 3 (20/07/2026 - 02/08/2026):** Complete the Backend business logic for Turn-based RPG Battles, Boss encounters, and Inventory/Item management.
*   **Milestone 4 (03/08/2026 - 15/08/2026):** Fully integrate the Unity Client with the Backend REST API, conduct comprehensive End-to-End (E2E) testing, and optimize AI response latency.

## 6. Budget Estimation

A massive advantage of this Serverless approach is the ability to leverage the AWS Free Tier extensively during the development and testing phases:
*   **AWS Cognito / Lambda / DynamoDB:** $0.00 (Comfortably within free tier limits).
*   **AWS Bedrock:** Charged per token used (Estimated at $1.00 - $5.00/month for testing traffic).
*   **Amazon API Gateway & CloudWatch:** Roughly $0.50 - $1.00/month.
*   **Estimated Total Cost:** **~$1.50 - $6.00 / month**. This is exceptionally cost-effective for a highly scalable multiplayer backend.

## 7. Risk Assessment

| Risk | Impact | Mitigation Strategy |
| :--- | :--- | :--- |
| **AI Response Latency** | High | Implement smooth "loading/typing" narrative animations on the Unity Client to mask API wait times. |
| **Malformed AI JSON Output** | Medium | The Backend utilizes strict Validator Modules and automatic Fallback/Retry mechanisms if the AI returns broken JSON structures. |
| **Exceeding Bedrock Token Limits** | Low | Configure strict `max_tokens` limits per API call and implement automated AWS Budget alerts. |

## 8. Expected Outcomes

*   **Revolutionary Player Experience:** Delivering a game that never feels old, with infinite replayability driven by Generative AI.
*   **A Standardized Architecture Framework:** Establishing a robust, reusable framework combining Unity and AWS .NET 8 Serverless. This codebase can serve as a foundation for future cloud-based games or interactive narrative applications.
*   **Operational Excellence:** Proving that a complex, high-traffic online game ecosystem can be developed and maintained with near-zero infrastructure costs in its initial stages.