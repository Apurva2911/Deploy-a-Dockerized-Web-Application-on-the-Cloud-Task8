
## 🐳Dockerized Web Application on the Cloud / Flask App Deployment on AWS ECS  

### 📘 Project Description

This project demonstrates how to **containerize a Flask web application** using Docker, push it to **Amazon Elastic Container Registry (ECR)**, and deploy it on **Amazon Elastic Container Service (ECS)** using Fargate. The application runs on a lightweight containerized infrastructure and displays a simple “Hello from ECS” message when accessed via the service URL.

---

### 🚀 Key Features

* Dockerized Flask web application
* Container image stored in **Amazon ECR**
* Deployment using **Amazon ECS (Fargate)**
* Configured **task definition, service, and cluster**
* Publicly accessible via ECS public IP or Load Balancer

---

### 🧱 Tech Stack

* **Backend:** Python (Flask)
* **Containerization:** Docker
* **Cloud Platform:** AWS ECS with Fargate
* **Registry:** Amazon ECR
* **Networking:** Security Groups, VPC, IAM Roles

---

### ⚙️ Steps to Reproduce
Create new directory

mkdir my-flask-app

cd my-flask-app

Add all files i.e app.py,requirements.txt,dockerfile in my-flask-app.

🐳 Push Image to AWS ECR

Build Docker Image Locally

docker build -t my-flask-app .

Check image:

docker images

Run container locally:

docker run -d -p 8080:8080 my-flask-app

Verify container:

docker ps

Visit in browser or EC2 public IP:

http://<your-ip>:8080

# Create ECR repo (if not created yet)
aws ecr create-repository --repository-name my-flask-app --region us-east-1

# Authenticate Docker with ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 424056759435.dkr.ecr.us-east-1.amazonaws.com

# Tag image
docker tag my-flask-app:latest 424056759435.dkr.ecr.us-east-1.amazonaws.com/my-flask-app:latest

# Push image
docker push 424056759435.dkr.ecr.us-east-1.amazonaws.com/my-flask-app:latest

#### 3️⃣ Deploy on ECS

* Create a new ECS **cluster** (Fargate).
* Define a **Task Definition** using the ECR image.
* Set **Container Port = 5000** (Flask default).
* Create a **Service** and run the task.
* Configure Security Group to allow inbound traffic on the exposed port (5000 or 8080).
---

### 🧩 Sample Dockerfile

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```
---

### 🧠 Verifying Deployment

* Visit the **Public IP or Load Balancer URL** shown in your ECS service.
* You should see:
  
  Hello from ECS Fargate!                                                        |


### 🧹 Cleanup (to avoid extra charges)

1. **Stop and delete ECS service**
2. **Delete ECS cluster**
3. **Deregister task definition**
4. **Delete ECR image and repository**
5. **Remove VPC/Security Groups** if created manually

👩‍💻 Author
Apurva Kadam
🎓 B.Tech in Computer Science
💡 Skilled in AWS, Docker, Python, and Cloud Deployment
📧 Contact: apurvak2911@gmail.com
🌐 GitHub: [github.com/ApurvaKadam](https://github.com/Apurva2911)
💬 “Passionate about learning, building, and automating cloud solutions.”
   
