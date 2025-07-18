# 🧠 Amazon Bedrock GenAI Workshop — Console Experience (RAG)

This repository walks you through building a **Retrieval-Augmented Generation (RAG)** application using **Amazon Bedrock Knowledge Bases**, and an **AI Agent with Code Interpreter**, using only the AWS **Management Console** — no coding required.

> 📌 **Workshop Source**: [AWS Bedrock Workshop](https://catalog.workshops.aws/amazon-bedrock/en-US)

---

## 📑 Table of Contents

- [What You’ll Learn](#-what-youll-learn)
- [Section 1 — Build a Knowledge Base (RAG Flow)](#-section-1--build-a-knowledge-base-rag-flow)
  - [Section 1.1 — Create a Vector Store with OpenSearch Serverless](#-section-11--create-a-vector-store-with-opensearch-serverless)
  - [Section 1.2 — Upload Source Documents to Amazon S3](#-section-12--upload-source-documents-to-amazon-s3)
  - [Section 1.3 — Create a Bedrock Knowledge Base](#-section-13--create-a-bedrock-knowledge-base)
  - [Section 1.4 — Test the Knowledge Base](#-section-14--test-the-knowledge-base)
  - [Section 1.5 — Build a RAG Flow with Bedrock Flows Visual Builder](#-section-15--build-a-rag-flow-with-bedrock-flows-visual-builder)
- [Section 2 — Create a Bedrock Agent with Code Interpreter](#-section-2--create-a-bedrock-agent-with-code-interpreter)
- [Resources](#-resources)

---

## 📋 What You’ll Learn

This workshop is ideal for users who prefer a **no-code experience**. You'll complete the following:

- ✅ Create an **Amazon OpenSearch Serverless** vector index
- ✅ Upload source documents to **Amazon S3**
- ✅ Set up and test a **Bedrock Knowledge Base**
- ✅ Build a **RAG Flow** using **Bedrock Flows Visual Builder**
- ✅ Create an **AI Agent** with **code interpreter** (Python execution + visualization)

---

## 🧠 Section 1 — Build a Knowledge Base (RAG Flow)

### 🚀 Section 1.1 — Create a Vector Store with OpenSearch Serverless

... *(content unchanged)* ...

### 📚 Configure the Knowledge Base Node

... *(content unchanged)* ...

---

## 🤖 Section 2 — Create a Bedrock Agent with Code Interpreter

This guide walks you through the process of creating an **AI agent with code interpretation capabilities** using the **Amazon Bedrock Console**. The agent will analyze data and generate visualizations — all through the no-code console UI.

### 🧰 Prerequisites

- An AWS account with access to Amazon Bedrock
- Familiarity with the AWS Management Console
- ✅ **Required**: Enable foundation models (e.g. Claude 3.5 Sonnet) in Model Access

### 🧭 Step-by-Step Instructions

#### 1️⃣ Access Amazon Bedrock Console

1. Sign in to the [AWS Console](https://console.aws.amazon.com/)
2. Navigate to **Amazon Bedrock**
3. Click **Agents** from the left navigation menu

#### 2️⃣ Create a New Agent

- Click **Create Agent**
- Name: `DataAnalysisAssistant`
- Description *(optional)*: `AI Agent with Code Interpreter enabled for Data analysis`
- Click **Create**

#### 3️⃣ Configure Agent Details

- Under **Agent Details**:
  - Select **Create and use a new service role**
  - Choose **Claude 3.5 Sonnet v2**
- Under **Instructions for the Agent**, enter:

```
You are an AI assistant specialized in data analysis and visualization. You can write, run, and debug Python code to help users with their queries. Always provide clear explanations of your process and results.
```

#### 4️⃣ Enable Code Interpreter

- Expand **Additional Settings**
- Toggle ✅ **Code Interpreter**
- Ensure **User Input** is enabled

#### 5️⃣ Save and Prepare Agent

- Review the settings
- Click **Save**
- Then click **Prepare** to activate the agent

#### 6️⃣ Test the Agent

In the test panel (right side), paste this prompt:

```
Using the customer satisfaction data provided below, create a bar graph showing the average overall rating for each hotel (H001, H002, H003). The graph should have the hotel IDs on the x-axis and the average overall rating on the y-axis.

date,hotel_id,overall_rating,room_cleanliness,staff_service,amenities,value_for_money,location
2023-01-05,H001,4.2,4.5,4.0,3.8,4.1,4.5
2023-01-12,H002,3.8,4.0,3.5,3.9,3.7,4.2
2023-01-20,H003,4.5,4.7,4.6,4.3,4.2,4.8
2023-02-03,H001,3.9,4.2,3.7,3.6,3.8,4.4
2023-02-15,H002,4.1,4.3,4.0,4.1,3.9,4.3
2023-02-28,H003,4.3,4.5,4.4,4.2,4.0,4.6
2023-03-10,H001,4.0,4.3,3.8,3.7,3.9,4.5
2023-03-22,H002,3.7,3.9,3.6,3.8,3.5,4.1
2023-04-05,H003,4.4,4.6,4.5,4.1,4.1,4.7
2023-04-18,H001,4.1,4.4,3.9,3.8,4.0,4.6
2023-05-01,H002,3.9,4.1,3.8,4.0,3.6,4.2
2023-05-15,H003,4.6,4.8,4.7,4.4,4.3,4.9
2023-06-02,H001,4.3,4.6,4.1,4.0,4.2,4.7
2023-06-20,H002,4.0,4.2,3.9,4.1,3.8,4.3
2023-06-30,H003,4.5,4.7,4.6,4.3,4.2,4.8
```

### 🧪 Additional Prompts for Testing

Try testing with these:

- Create a heatmap that displays the correlation between satisfaction factors and overall rating
- Calculate the average scores for each satisfaction factor across all hotels
- Identify the hotel with the highest average rating and show its factor scores
- Create a line graph showing the trend of overall ratings over time

📌 **Ensure all graphs are well labeled and easy to read.**

---

## ✅ Conclusion

You've now created two end-to-end GenAI experiences using **Amazon Bedrock**, entirely through the console — no code required:

- A RAG pipeline using **Knowledge Bases + Flows**
- A powerful **AI Agent** with **Python code interpreter** for real-time analysis

---

## 📚 Resources

- [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock)
- [Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service)
- [Knowledge Bases Overview](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html)
- [Bedrock Agents Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html)

