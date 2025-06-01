# Generative AI Application using Amazon Bedrock

This repository contains notes and key concepts from the **"Generative AI Application using Amazon Bedrock"** course provided by **AWS Skill Builder**. It also includes theoretical overviews of the AWS services used in generative AI application development.

---

## 📘 Course Overview

The course introduces the fundamentals of generative AI and how to build applications using **Amazon Bedrock**, a managed service that provides access to foundation models (FMs) from top AI model providers through a unified API.

---

## 🧠 What I Learned

- Core concepts of **Generative AI** and its real-world use cases
- How to build GenAI apps using **Amazon Bedrock**
- Working with **Foundation Models (FMs)** for:
  - Text generation
  - Image generation
- Prompt engineering and model evaluation
- Building GenAI workflows with:
  - **Python (Boto3)**
  - **LangChain**
- Deploying applications with:
  - **AWS Lambda**
  - **API Gateway**
  - **Amazon S3 & SageMaker**

---

## ☁️ AWS Services – Theory Overview

### 🔹 Amazon Web Services (AWS)
AWS is a cloud platform offering compute power, storage, databases, machine learning, and more. It allows developers to build and deploy applications globally without managing physical servers.

### 🔹 Amazon S3 (Simple Storage Service)
- Object storage service used for storing data like files, images, logs, and backups.
- Supports scalability, high availability, and durability.
- Common use cases: static website hosting, data lake, file uploads.
- In GenAI, S3 is used to store input/output data such as documents, prompts, and results.

### 🔹 AWS Lambda
- Serverless compute service that runs your code in response to events.
- No need to provision or manage servers.
- Supports languages like Python, Node.js, Java, etc.
- Useful in GenAI apps for tasks like triggering model inference, file processing, or data transformation.

### 🔹 Amazon API Gateway
- Fully managed service to create, publish, and secure REST and WebSocket APIs.
- Acts as an interface between front-end clients and back-end services (e.g., Lambda).
- Useful for exposing generative AI functions as public or private APIs.

### 🔹 Amazon Bedrock
- Fully managed service to access foundation models from providers like Anthropic (Claude), Amazon (Titan), Stability AI, Meta (Llama), and others.
- Enables text generation, summarization, Q&A, image generation, and more.
- No need to manage infrastructure or train models.
- Easy integration with other AWS services.

### 🔹 Amazon SageMaker (Optional for advanced users)
- Managed service to build, train, and deploy ML models at scale.
- Useful for custom model fine-tuning or hosting if needed beyond Bedrock's capabilities.

---

## 🛠️ Tools & Technologies

- **Amazon Bedrock**
- **Boto3 (AWS SDK for Python)**
- **LangChain (for orchestration and chaining prompts)**
- **Amazon Lambda, S3, API Gateway**
- **CloudWatch (for monitoring Lambda/API calls)**

---

## 🎯 Key Takeaways

- Serverless architecture with secure and scalable AI integration
- Access to best-in-class models without needing ML expertise
- Easy deployment of intelligent applications using AWS-native tools

---

## ✅ Course Completion

This course was successfully completed on **AWS Skill Builder** as part of my learning journey into Generative AI.

---
