# BLOG GENERATION GENERATIVE AI APP USING AMAZON BEDROCK

````markdown
# 🧠 AI Agent for Blog Generation using Amazon Bedrock

This project demonstrates how to build a **Generative AI agent application** using **Amazon Bedrock** with the **Meta LLaMA3-8B-Instruct model**. It allows users to generate blog content based on a given topic, using an API-driven architecture powered by **AWS Lambda**, **Amazon API Gateway**, **Amazon S3**, and **CloudWatch**.

---

## 📌 Project Architecture

**High-Level Flow:**

1. A client (e.g., Postman) sends an API request with a blog topic.
2. API Gateway routes the request to AWS Lambda.
3. Lambda invokes the LLaMA 3 model from Amazon Bedrock to generate a blog.
4. The generated blog is:
   - Logged in CloudWatch
   - Saved as a `.txt` file in an S3 bucket

![image](https://github.com/user-attachments/assets/e9745e46-847d-49ae-9ae9-966fb8023acc)

---

## 🛠️ AWS Services Used

### ✅ Amazon Bedrock
- Provides access to foundation models like `meta.llama3-8b-instruct-v1:0`.
- Used to generate blog content based on input topics.
![WhatsApp Image 2025-06-01 at 20 38 28_a2935436](https://github.com/user-attachments/assets/51c39dce-dc44-4c01-82c6-e35d18a0a0d4)
- here we have used the meta llama3-8b  FM model to generate the blog content here are the detailsof the model:
![WhatsApp Image 2025-06-01 at 20 37 44_41d5a30c](https://github.com/user-attachments/assets/f3142d6c-158d-4d68-ae8b-158eb60ba143)


### ✅ AWS Lambda
- Handles API requests and runs the logic for calling the model and storing results.
![WhatsApp Image 2025-06-01 at 20 35 35_1c2a2d10](https://github.com/user-attachments/assets/3e0ec553-5e5b-4b4d-a47b-6d812b105630)
- here we have the lambda function which is connected with the API gateway so once the user hits the post api it will land to lambda function via API Gateway.
- lambda function code Written in Python using the `boto3` and `botocore` libraries.
![WhatsApp Image 2025-06-01 at 20 36 03_0679470c](https://github.com/user-attachments/assets/74a4aee2-2ec8-478a-8ea1-6172c1ebb5ee)

### ✅ Amazon API Gateway
- Exposes the Lambda function as a RESTful API.
- Routes incoming requests securely and efficiently.
![WhatsApp Image 2025-06-01 at 20 39 16_27178f6e](https://github.com/user-attachments/assets/3671f633-aa70-461a-b0ef-abafbebf1dfe)
![WhatsApp Image 2025-06-01 at 20 39 34_e2f572de](https://github.com/user-attachments/assets/45f3e54d-d196-45b4-afbb-54e011bcbd1b)
- here we have created our dev environment and deploy it.you can see the invoke api url https://qzazbm4zbf.execute-api.us-east-1.amazonaws.com/dev/blog-generation. so once user send the api call with body it invoke blog_topics and go to lambda function.
![image](https://github.com/user-attachments/assets/f21d6e6b-cddc-4f9a-82c8-a27430382411)


### ✅ Amazon S3
-created the s3 bucket storage in AWS S3
![WhatsApp Image 2025-06-01 at 20 39 57_23858533](https://github.com/user-attachments/assets/e6ec5b9d-2c6a-4011-8eca-0c3d5c0aa6c1)
- Stores the generated blogs in text format under the `blog-output/` prefix.
![WhatsApp Image 2025-06-01 at 20 40 16_ef84cd2d](https://github.com/user-attachments/assets/c7c5b39b-4966-4294-84ac-1f920c56140c)
- Used as persistent storage for blog content.
![WhatsApp Image 2025-06-01 at 20 41 57_46226c08](https://github.com/user-attachments/assets/2b8bad33-1c62-460a-b3d8-c758103da826)


### ✅ Amazon CloudWatch
- Used for logging and monitoring Lambda function execution.
![WhatsApp Image 2025-06-01 at 20 35 00_ee68d0cd](https://github.com/user-attachments/assets/24e8a5af-1ca9-4c43-9333-5932863a4583)
- Helps track API calls and model response status.

---

## 🧑‍💻 Lambda Function Code Overview

```python
def blog_generate_using_bedrock(blogtopic: str) -> str:
    prompt = f"""<s>[INST]Human: Write a 300 words blog on the topic {blogtopic}
    Assistant:[/INST]"""
    
    body = {
        "prompt": prompt,
        "max_gen_len": 512,
        "temperature": 0.5,
        "top_p": 0.9
    }

    bedrock = boto3.client("bedrock-runtime", region_name="us-east-1")
    response = bedrock.invoke_model(body=json.dumps(body), modelId="meta.llama3-8b-instruct-v1:0")
    response_data = json.loads(response.get('body').read())
    return response_data['generation']
````

* Generates blog content using Meta's LLaMA3 model via Bedrock.
* Stores output in a specified S3 bucket under a time-stamped key.

---

## 🚀 Steps to Deploy

1. **Create S3 Bucket**

   * Name: `aws_bedrock_course1`
   * Folder: `blog-output/`

2. **Create Lambda Function**

   * Runtime: Python 3.9+
   * Paste the provided Lambda code
   * Add permissions for S3 and Bedrock access

3. **Create API using API Gateway**

   * Method: `POST`
   * Integration: Lambda
   * Deploy and copy the endpoint URL

4. **Invoke API**

   * Use Postman or any HTTP client
   * Set method to `POST`
   * Provide a JSON body:

     ```json
     {
       "blog_topic": "The Future of Artificial Intelligence"
     }
     ```

---

## 📂 Example Output

* **S3 Location:** `blog-output/123456.txt`
* **Content:** 300-word blog generated by Meta LLaMA3

---

## 📈 Monitoring

* View logs and errors via **Amazon CloudWatch Logs**.
* Track model latency, input/output, and failures.

---

## ✅ Status

✅ Fully deployed and tested
✅ Model integrated with Bedrock
✅ API accessible via API Gateway
✅ Blogs stored in S3 successfully

---

## 📚 Learning Outcomes

* Hands-on experience with Amazon Bedrock and foundation models
* Serverless application design using AWS Lambda and API Gateway
* Using boto3 to interact with Bedrock and S3
* Real-world use case: Blog content generation with GenAI

---

## 📦 Tech Stack

| Component       | Tech/Service               |
| --------------- | -------------------------- |
| Backend Logic   | AWS Lambda (Python)        |
| Model Inference | Amazon Bedrock (LLaMA3-8B) |
| Storage         | Amazon S3                  |
| API Interface   | Amazon API Gateway         |
| Monitoring      | Amazon CloudWatch          |
| API Testing     | Postman                    |

---

## 🔒 Note

This project is for educational purposes and demonstrates a typical GenAI use case using AWS services. Always secure your APIs before production deployment.

---

