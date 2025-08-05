
I have developed a fully robust CI/CD pipeline for a Django-React based Notes App. This pipeline automates the entire process from code push to deployment using the following components:

- **Dockerized Setup**: Both frontend (React) and backend (Django) are containerized using Docker.
- **Declarative Jenkins Pipeline**: Built using a Jenkinsfile with Declarative syntax for better readability and maintainability.

## Stages in Pipeline:

- SCM Checkout
- Trivy Security Scan: Performs a file system scan using Trivy to detect vulnerabilities before building the Docker image
- Docker Image Build
- Automated Testing
- Push to DockerHub
- Deployment to server
- Post-build Actions

- **GitHub Webhook Integration**: Automatically triggers Jenkins build on every push to the GitHub repository.
- **DockerHub Integration**: Built images are pushed to DockerHub and pulled by the deployment server.
- **Email Notification**: Sends build status alerts (success/failure) after each run.
- **Efficient Runtime**: Average total pipeline runtime is ~33 seconds as seen in the Jenkins Stage View.

This setup ensures smooth, automated, and error-free deployment, making the project DevOps-ready and production-friendly.



## Requirements
1. Python 3.9
2. Node.js
3. React

## Prerequisites

Before you begin, make sure you have the following installed:

- Docker
- Git (optional, for cloning the repository)

## Setup

1. Clone this repository (if you haven't already):

   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   ```

2. Navigate to the project directory:

   ```bash
   cd your-repo-name
   ```

3. Create a `.env` file in the project root with the following content:

```dotenv
DB_NAME=test_db
DB_USER=root
DB_PASSWORD=root
DB_PORT=3306
DB_HOST=db_cont


   ```

## Usage

1. Start the containers using Docker Compose:
   ```bash
   sudo apt-get install docker-compose-v2
   ```
 
   ```bash
   docker-compose up -d
   ```

2. Access the Flask app in your web browser:

   - Frontend: http://localhost
   - Backend: http://localhost:5000

## Nginx

Install Nginx reverse proxy to make this application available

`sudo apt-get update`
`sudo apt install nginx`






```
#  GitOps Pipeline (demo-cicd) using Jenkins 🚀

**Automated Jenkins CI/CD Pipeline triggered by GitHub Webhook**

Jab bhi koi developer `git push` karta hai **GitHub** par, **Jenkins** automatically:

1. `Checkout` — latest code pull karta hai  
2. `Build` — project compile / package karta hai  
3. `Test` — automated tests chalata hai  
4. `Deploy` — target server ya cloud par code release karta hai  

*Docker image build/push yahan cover **nahin** kiya gaya, kyunki aap ne mana kiya hai.*

---

## 🛠️ Prerequisites

| Requirement | Why Needed |
|-------------|------------|
| **Jenkins (LTS)** + *Git* & *Pipeline* plugins | CI/CD engine |
| **GitHub Repo** | Source code aur Webhook trigger |
| **Public URL** (e.g. server IP ya Ngrok) | GitHub ➜ Jenkins webhook delivery |
| Optional: Credentials | Private repo clone ya deploy target ke liye |

---


---
## Set up Jenkins
### ✅ Step 1: Install Java (Required for Jenkins)

```bash
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
```

🔍 **Check Java Version**
```bash
java -version
```
✅ Output:
```
openjdk version "21.0.3" 2024-04-16
```

---

### ✅ Step 2: Add Jenkins Repository & Install (Stable LTS)

```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" \
  | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins -y
```

---

### ✅ Step 3: Start Jenkins Service

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

📍 Access Jenkins on: `http://<your-server-ip>:8080`

---




## 🔐 Jenkins Credentials Setup

1. Go to **Jenkins Dashboard > Manage Jenkins > Credentials > Global > Add Credentials**.
2. Choose:
   - **Kind**: `Username with password`
   - **Username**: Your Docker Hub username
   - **Password**: create a personal access token and give this token
   - **ID**: `dockerhub`
3. Click **create**

---





## ⚡ Quick Start or  webhooks set-up

1. **Webhook create karo**   
   GitHub → *Settings* → *Webhooks* →  
   **Payload URL**: `http://<jenkins-ip>:8080/github-webhook/`  
   Content‑Type: `application/json`, Event: **Just the push event**

2. **Jenkins me Pipeline Job banao**  
   - *New Item* → **Pipeline** → Name: `demo-cicd`  
   - *Build Triggers*: ✅ **GitHub hook trigger for GITScm polling**  
   - *Pipeline script from SCM* → Repo URL & branch set karo → `Jenkinsfile` path confirm karo

3. **Jenkinsfile** repo ke root me already present hai. Zaroorat ho to build/test commands modify karo.

4. `git push` karo → Jenkins pipeline turant run hoga.

---

## 📂 Directory Structure

```
.
├── Jenkinsfile
└── src/  (aapka source code yahan)
```

---

---

## 🧩 Troubleshooting Tips

- **Webhook 404**: Jenkins URL galat ya port firewall me blocked?  
- **Build Fail**: Console log padho, dependencies check karo.  
- **Tests Skip**: Test scripts executable & path sahi hai?  
- **Deploy Issues**: Credentials & target server permissions verify karo.

---
---

### 🐳 Successfully pushed the containerized Flask application to Docker Hub  
This image is automatically built and deployed through the Jenkins pipeline.

<img width="1920" height="1080" alt="Screenshot (78)" src="https://github.com/user-attachments/assets/2889d050-2f83-451e-a9f7-44e1eacb6324" />

---

### 🔁 End-to-end Jenkins Pipeline  
Triggered by GitHub pushes — automates pull → build → push to Docker Hub → deploy on EC2 using `docker-compose`.

<img width="1909" height="961" alt="Screenshot 2025-08-05 115805" src="https://github.com/user-attachments/assets/b6c9b820-e1ec-4a27-bff7-6aad1a6d13c7" /># CI/CD Pipeline Overview for Simple Notes App




---

### 🗄️ rules in AWS

<img width="1917" height="951" alt="Screenshot 2025-08-05 112426" src="https://github.com/user-attachments/assets/74b3270c-55a8-446c-9e73-b29916cefdfd" />

<img width="1918" height="906" alt="Screenshot 2025-08-05 120112" src="https://github.com/user-attachments/assets/413a5786-c34c-4fc1-95e0-87958170196a" />



---



---

### 🗄️ Jenkins Setup

<img width="1920" height="1080" alt="Screenshot (86)" src="https://github.com/user-attachments/assets/aa8a3a6a-05ec-47f3-887f-21d7f6b256b4" />
<img width="1920" height="1080" alt="Screenshot (87)" src="https://github.com/user-attachments/assets/6f35c573-1d3c-4b63-9bd5-c7427a81d940" />



---




---
- **Live Flask web app UI connected to MySQL backend.
User-submitted messages are stored and fetched from the database in real time.

<img width="1670" height="922" alt="Screenshot 2025-08-03 100911" src="https://github.com/user-attachments/assets/c733504e-9e75-4254-aba4-1927168315f8" />

---

### 🗄️ Emil Notification 
<img width="1919" height="956" alt="Screenshot 2025-08-05 112710" src="https://github.com/user-attachments/assets/9d488c7f-7d3c-48bc-82ce-1b00b5aa4055" />


<img width="1915" height="822" alt="Screenshot 2025-08-05 112336" src="https://github.com/user-attachments/assets/a1c01d7a-34e4-43a0-a08c-d4394a2b7c24" />

<img width="1078" height="548" alt="Screenshot 2025-08-05 112206" src="https://github.com/user-attachments/assets/c7ff0e51-b12c-40f3-b89d-199b32a917b9" />






---

## 🔁 CI/CD Flow Summary

Jab bhi koi developer GitHub par `git push` karta hai:

1. **SCM Trigger**: GitHub webhook se Jenkins ko signal milta hai
2. **Code Checkout**: Jenkins GitHub se latest code clone karta hai
3. **Trivy File System Scan: Jenkins trivy fs . -o results.json command se security vulnerabilities ke liye codebase scan karta hai
4. **Build**: Flask app ke liye dependencies install karta hai / test run karta hai
5. **Docker Build**: Jenkins Docker image banata hai Flask app ke liye
6. **Push to Docker Hub**: Jenkins Docker image ko DockerHub par push karta hai
7. **Deploy via Docker Compose**: Remote server par Docker Compose file run karke Nginx + Django + Mysql containers deploy karta hai
8. **Email Notification: Jenkins deployment ke baad developer ko build status (Success/Failure) ka email bhejta hai

---

## 🙌 Credits

Made with 💛 by *Ajay Mall*.  
Feel free to raise an issue or PR!

---
