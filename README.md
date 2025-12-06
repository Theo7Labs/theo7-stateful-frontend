# Theo7 Stateful Visit Counter — Serverless Application (AWS + Netlify)

This project is a **fully functional serverless application** demonstrating how to maintain *state* in a stateless architecture using AWS.

The frontend is a single-page HTML interface deployed on **Netlify**, and the backend uses:

- **AWS Lambda (Python 3.11)**
- **Amazon DynamoDB**
- **API Gateway**
- **IAM Roles**
- **AWS SAM (Serverless Application Model)** for deployment

---

## 🔗 Live Demo  
Click below to use the live stateful counter:

👉 **https://theo7-visit-counter.netlify.app/

Each time you click the button, it calls your API Gateway endpoint, which triggers the Lambda and updates DynamoDB in real time.

---

## 🧠 What This Project Demonstrates

### ✔ Maintaining state in a stateless environment  
Serverless functions (Lambda) do not persist memory between executions.  
This project solves that by storing the visit count in DynamoDB using a unique `session_id`.

### ✔ Read → Modify → Write pattern  
The Lambda function performs:

1. **Read State:** Fetch current `visit_count` from DynamoDB  
2. **Modify State:** Increment the counter  
3. **Write State:** Save back to DynamoDB

### ✔ Decimal type bug resolution  
DynamoDB stores numbers as `Decimal`.  
A bug was fixed by converting to Python `int()` before JSON serialization.

### ✔ Real-world debugging skills  
Using CloudWatch logs to diagnose:
- Serialization errors  
- Environment variable issues  
- OneDrive sync conflicts with AWS SAM build folder  

---

## 🏗️ Architecture Overview


- The frontend sends requests to the AWS API.
- Lambda executes the logic.
- DynamoDB stores the persistent visit count.

---

## 🗂️ Code Structure

### Frontend (this repo)
- `index.html` — Tailwind-powered UI + inline JS hitting the API.

### Backend (in separate AWS SAM repo)
- `template.yaml` — Defines Lambda, API Gateway, IAM permissions, DynamoDB table.
- `app.py` — Lambda handler implementing the stateful counter.

---

## 🚀 Deployment Summary

### **Frontend**
- Hosted for free on **Netlify**
- Zero build step (pure static HTML)

### **Backend**
- Deployed with `sam build` and `sam deploy`
- Uses environment variables to connect Lambda → DynamoDB
- DynamoDB table stores visit counts using `session_id` as the key

---

## 👤 Author  
Built by **Theo7 Labs**  
Exploring cloud engineering, serverless patterns, and real-world AWS projects.
