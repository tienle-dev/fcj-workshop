---
title: "Week 3 Worklog"
date: 2026-07-06
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Design & Manipulate Game Database (DynamoDB / RDS).

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| Mon | - Survey and choose the database type (NoSQL vs SQL) suitable for game mechanics.<br>- Design table structures: Account (User) and Character (Character). | 07/06/2026 | 07/06/2026 |
| Tue | - Design storage structures: Item (Inventory), Story Progress (StorySession), and Match (Battle). | 07/07/2026 | 07/07/2026 |
| Wed | - Initialize DynamoDB (or RDS) tables on the AWS Console.<br>- Setup key structures (Primary Key, Partition Key) to optimize queries. | 07/08/2026 | 07/08/2026 |
| Thu | - Configure Secondary Indexes (GSI) for DynamoDB tables to serve complex search features. | 07/09/2026 | 07/09/2026 |
| Fri | - Write Repository classes in C# for the Backend.<br>- Perform CRUD (read/write) operations for real-time game state data. | 07/10/2026 | 07/11/2026 |

### Week 3 Achievements:

Week 3 focused on shaping how to efficiently store and manage game data, ensuring fast retrieval speeds and easy scalability. I completed the following tasks:

* **Comprehensive Database Structure Design:** Analyzed and designed the data model for the entire game, including Player Account (User) information, Character (Character) states, Inventory (Inventory), Story Progress history (StorySession), and Match logs (Battle).
* **DynamoDB / RDS Initialization & Optimization:** Created tables in the actual AWS environment. Carefully configured Primary Keys, Partition Keys, and Global Secondary Indexes (GSIs) to optimize read/write capacity units, thereby saving costs and speeding up queries.
* **C# Repository Construction:** Completed the Data Access layer in the Backend architecture by writing Repository classes in C#. These functions safely handle continuous read/write operations of the game state (e.g., saving experience points, adding items to the inventory).

  ![Database Schema or DynamoDB Tables](/images/week3/database_schema.png)
  *(Note: Need to add database design schema or DynamoDB interface image here)*

  ```csharp
  // Repository class structure for Database manipulation - Illustration
  ```
  *(Note: Insert a typical C# Repository code snippet here)*
