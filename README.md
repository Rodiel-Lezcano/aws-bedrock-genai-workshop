# 🧠 Amazon Bedrock GenAI Workshop — Console Experience (RAG)

This repository walks you through building a **Retrieval-Augmented Generation (RAG)** application using **Amazon Bedrock Knowledge Bases**, focusing entirely on the AWS **Management Console**—no coding required.

> 📌 **Workshop Source**: [AWS Bedrock Workshop - RAG Console Path](https://catalog.workshops.aws/amazon-bedrock/en-US)

---

## 📑 Table of Contents

- [What You’ll Learn](#-what-youll-learn)
- [Section 1.1 — Create a Vector Store with OpenSearch Serverless](#-section-11--create-a-vector-store-with-opensearch-serverless)
- [Section 1.2 — Upload Source Documents to Amazon S3](#-section-12--upload-source-documents-to-amazon-s3)
- [Section 1.3 — Create a Bedrock Knowledge Base](#-section-13--create-a-bedrock-knowledge-base)
- [Section 1.4 — Test the Knowledge Base](#-section-14--test-the-knowledge-base)
- [Section 3.1 — Build a RAG Flow with Bedrock Flows Visual Builder](#-section-31--build-a-rag-flow-with-bedrock-flows-visual-builder)
- [Workshop Complete](#-workshop-complete)
- [Resources](#-resources)

---

## 📋 What You’ll Learn

This workshop is ideal for users who prefer a **no-code experience**. You'll complete the following:

- ✅ Set up an **Amazon OpenSearch Serverless** vector index
- ✅ Upload source documents to **Amazon S3**
- ✅ Create and configure a **Bedrock Knowledge Base** (via Console)
- ✅ Use **RetrieveAndGenerate API** via the AWS Console UI
- ✅ Build an **end-to-end RAG workflow** using **Bedrock Flows Visual Builder**

---

## 🚀 Section 1.1 — Create a Vector Store with OpenSearch Serverless

### 🧱 Step 1: Create an OpenSearch Vector Collection

1. Navigate to **Amazon OpenSearch Service** in the AWS Console.
2. On the left menu, go to **Serverless** → Click **Dashboard**.
3. Click **Get Started**.
4. Enter the following:
   - **Collection Name**: `bedrock-sample-rag`
   - **Collection Type**: `Vector Search`
   - **Deployment Type**: ✅ Enable Redundancy
   - **Security**: ✅ Easy Create
5. Click **Next**, then **Submit** to create the collection.

### 🧲 Step 2: Create the Vector Index

1. After the collection is created, go to the **Indexes** section.
2. Click **Create Vector Index**.
3. Choose **JSON** mode.
4. Use the following configuration:

```json
{
  "settings": {
    "index.knn": "true",
    "number_of_shards": 1,
    "knn.algo_param.ef_search": 512,
    "number_of_replicas": 0
  },
  "mappings": {
    "properties": {
      "vector": {
        "type": "knn_vector",
        "dimension": 1024,
        "method": {
          "name": "hnsw",
          "engine": "faiss",
          "space_type": "l2"
        }
      },
      "text": {
        "type": "text"
      },
      "text-metadata": {
        "type": "text"
      }
    }
  }
}
```

5. Name your index: `bedrock-sample-rag-index`
6. Click **Create**

### 🧾 Important Metadata to Save

| Property              | Value                       |
|-----------------------|-----------------------------|
| **Index Name**        | `bedrock-sample-rag-index` |
| **Vector Field Name** | `vector`                   |
| **Metadata Fields**   | `text`, `text-metadata`    |
| **Collection ARN**    | _Save this from Console_   |

---

## 📂 Section 1.2 — Upload Source Documents to Amazon S3

### 🧾 Step-by-Step Instructions

1. **Download the following documents** to your local directory:
   - `AMZN-2019-Shareholder-Letter`
   - `AMZN-2020-Shareholder-Letter`
   - `AMZN-2021-Shareholder-Letter`
   - `AMZN-2022-Shareholder-Letter`

2. **Upload these documents** to an S3 bucket.

   ✅ **Recommended Bucket Name**: `aws-bedrock-kb-workshop-aoss`  
   *(Choose a unique name if it’s your first time — e.g., `bedrock-kb-rodiel-lab`)*

---

## 🧠 Section 1.3 — Create a Bedrock Knowledge Base

### 🏗️ Step-by-Step Instructions

1. Go to the Amazon Bedrock Console.
2. In the left panel, click Builder Tools → Knowledge Bases.
3. Click **Create** and choose *Knowledge base with vector store*.

### 🔐 IAM Permissions

- Ensure **Create and use a new service role** is selected.

### 📤 Data Source

- Choose **Amazon S3** as the data source.
- Click **Browse S3** and select the bucket from Section 1.2.
- Under Chunking strategy:
  - Select: Fixed-size chunking
  - Set Max tokens: 512
- Click **Next**.

### 🧬 Embeddings Model

1. Click **Select Model**.
2. Choose: **Amazon Titan Text Embeddings V2**.
3. Click **Apply**.

### 🧲 Vector Database Configuration

- Choose the previously created OpenSearch vector store.
- Ensure **Vector engine for Amazon OpenSearch** is selected.

| Property             | Value                         |
|----------------------|-------------------------------|
| **Collection ARN**   | (Use ARN from Section 1.1)    |
| **Vector Index Name**| `bedrock-sample-rag-index`    |
| **Vector Field Name**| `vector`                      |
| **Text Field Name**  | `text`                        |
| **Metadata Field Name**| `text-metadata`            |

Click **Next** to continue.

### ✅ Finalize

- In the Review and Create section, click **Create Knowledge Base**.
- After it’s created, go to the **Data Sources** tab.
- Select your source and click **Sync** to ingest documents into the knowledge base.

---

## 🧪 Section 1.4 — Test the Knowledge Base

### 🧠 Step-by-Step Testing

1. Go to your Knowledge Base in the Bedrock Console.
2. Click **Test Knowledge Base** from the UI.
3. Click **Select Model** → Choose: **Anthropic**, select **Claude 3.5 Haiku** → Click **Apply**

### 📝 Sample Query

Paste this question in the input field and click **Run**:

```
What is Amazon doing in the field of generative AI?
```

### 🔍 View Results

- Click **Show Details** after generating a response.
- Under **Source Details**, inspect:
  - Extracted data chunks
  - Metadata used in generating the answer

---

## 🔄 Section 3.1 — Build a RAG Flow with Bedrock Flows Visual Builder

Create a Bedrock Flow that connects a Knowledge Base to a prompt template for dynamic, real-time question answering.

### 🧭 Step-by-Step Instructions

1. Go to the Amazon Bedrock Console → Click **Flows**.
2. Click **Create Flow**.
3. Enter Flow Name: `langchain-kb-retriever`
4. Under Service role name, select **Create and use a new service role**.
5. Click **Create Flow**.

### 🎯 Configure the Flow Builder

You’ll now see 3 nodes:
- Flow input
- Prompt
- Flow output

👉 Add a **Knowledge Base** node from the menu.

### 🧩 Configure the Prompt Node

1. Click the Prompt Node → **Select Model**: *Amazon Titan - Nova Micro*
2. Paste the following prompt:

```
Human: You are a financial advisor AI system, and provide answers to questions using fact-based and statistical information when possible.  
Use the following pieces of information to provide a concise answer to the question enclosed in <question> tags.  
If you don't know the answer, just say that you don't know; don't try to make up an answer.

<question>
{{question}}
</question>

The response should be specific and use statistics or numbers when possible.

Context: {{context}}

A:
```

3. Scroll to **Prompt Settings** → Change *context input type* to **Array**.

### 📚 Configure the Knowledge Base Node

1. Select the Knowledge Base created in Section 1.3
2. Enable: ✅ *Return retrieved results*

### 🔗 Connect the Nodes

```
Flow input → Prompt ({{question}})
Flow input → Knowledge Base (retrieval query)
Knowledge Base output → Prompt ({{context}})
Prompt output → Flow output
```

✅ Click **Save** once connected.

### 🧪 Test the Flow

1. Click on the **Test Panel** icon
2. Use this prompt:

```
What is Amazon doing in the field of generative AI?
```

📊 View the trace across nodes to confirm each step worked correctly.

---

## 🎉 Workshop Complete

You’ve created a fully no-code GenAI workflow using Amazon Bedrock, combining:
- Amazon S3
- Amazon OpenSearch Serverless
- Titan Embeddings
- Bedrock Knowledge Bases
- Bedrock Flows
- Claude and Titan models

---

# 🤖 Amazon Bedrock Workshop — Configuring Bedrock Agent via Console

This guide walks you through the process of creating an **AI agent with code interpretation capabilities** using the **Amazon Bedrock Console**. The agent will analyze data and generate visualizations — all through the no-code console UI.

---

## 🧰 Prerequisites

- An AWS account with access to Amazon Bedrock
- Familiarity with the AWS Management Console
- **Required**: Enable foundation models (e.g. Claude 3.5 Sonnet) in Model Access

---

## 🧭 Step-by-Step Instructions

### 1️⃣ Access Amazon Bedrock Console

1. Sign in to the [AWS Console](https://console.aws.amazon.com/)
2. Navigate to **Amazon Bedrock**
3. Click **Agents** from the left navigation menu

---

### 2️⃣ Create a New Agent

- Click **Create Agent**
- Name: `DataAnalysisAssistant`
- Description *(optional)*: `AI Agent with Code Interpreter enabled for Data analysis`
- Click **Create**

---

### 3️⃣ Configure Agent Details

- Under **Agent Details**:
  - Select **Create and use a new service role**
  - Choose **Claude 3.5 Sonnet v2**
- Under **Instructions for the Agent**, enter:

```txt
You are an AI assistant specialized in data analysis and visualization. You can write, run, and debug Python code to help users with their queries. Always provide clear explanations of your process and results.
```

---

### 4️⃣ Enable Code Interpreter

- Expand **Additional Settings**
- Toggle ✅ **Code Interpreter**
- Ensure **User Input** is enabled

---

### 5️⃣ Save and Prepare Agent

- Review the settings
- Click **Save**
- Then click **Prepare** to activate the agent

---

### 6️⃣ Test the Agent

In the test panel (right side), paste this prompt:

```txt
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

---

## 🧪 Additional Prompts for Testing

Try testing with these:

- Create a heatmap that displays the correlation between satisfaction factors and overall rating
- Calculate the average scores for each satisfaction factor across all hotels
- Identify the hotel with the highest average rating and show its factor scores
- Create a line graph showing the trend of overall ratings over time

📌 **Ensure all graphs are well labeled and easy to read.**

---

## ✅ Conclusion

You've now built and tested an **Amazon Bedrock Agent with Code Interpreter**, fully through the console — no code required.

This agent can:
- Analyze structured data
- Generate graphs and charts
- Explain results with Python + natural language

## 📚 Resources

- [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock)
- [Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service)
- [Knowledge Bases Overview](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html)
