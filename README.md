# sns-project
Thanks for sharing the **complete project overview**. This is a clean and systematic walk-through of how to **send emails via AWS SNS using Node.js hosted on an EC2 instance** with a web form interface.

To summarize, this is what your project does:

---

## ✅ **Project Goal**

> Create a web app hosted on an EC2 instance that lets users send emails via AWS SNS by filling out a form.

---

## 🔧 **High-Level Setup Steps**

### 1. **Create SNS Topic and Subscription**

* Created SNS topic (`DEMOSNS`)
* Subscribed an email address to the topic (via email confirmation)

---

### 2. **EC2 Setup**

* Launched Amazon Linux instance
* Installed Node.js (v16) using:

  ```bash
  curl -sL https://rpm.nodesource.com/setup_16.x | sudo bash -
  sudo yum install -y nodejs
  ```
* Verified with `node -v` and `npm -v`

---

### 3. **Node.js Project Initialization**

* Created project folder:

  ```bash
  mkdir snsproject && cd snsproject
  ```
* Initialized Node project:

  ```bash
  npm init -y
  ```
* Installed dependencies:

  ```bash
  npm install express aws-sdk body-parser
  ```

---

### 4. **Created `app.js` Backend API**

* Accepts POST requests to `/send-email`
* Publishes a message to SNS Topic
* Required environment:

  * `AWS.config.region` set
  * SNS Topic ARN set

---

### 5. **Created Frontend (`index.html`)**

* A clean HTML form using POST via JavaScript fetch API
* Collects email, subject, and message
* Sends to `/send-email`

---

### 6. **Installed PM2 to Run App in Background**

```bash
npm install -g pm2
pm2 start app.js --name "my-app1"
pm2 list
```

---

### 7. **Security Groups and Port Access**

* Edited inbound rules:

  * **Custom TCP Rule**: port 3000 open to `0.0.0.0/0`
* Accessed app on: `http://<your-ec2-public-ip>:3000`

---

### 8. **IAM Role and Permissions**

* Created IAM role with `AmazonSNSFullAccess`
* Attached IAM role to EC2 instance
* This allows EC2 to publish messages to SNS without needing explicit credentials

---

### 9. **Final Testing**

* After IAM role is added → Form submits successfully
* Email arrives in subscribed inbox

---

## ✅ **Project Done!**

### 👇 Key Concepts You Covered:

* AWS SNS topic and email subscription
* EC2 + Node.js web app deployment
* Form handling with fetch API
* IAM role for secure access to AWS services
* Port and security group configuration
* Background Node process with PM2

---

## 🛠️ Suggestions for Improvement

If you're planning to expand or refine this project:

### 1. **Form Validation**

* Check if fields are empty in JS before sending

### 2. **Environment Variables**

* Store region and SNS ARN in a `.env` file
* Use `dotenv` package:

  ```bash
  npm install dotenv
  ```

  ```js
  require('dotenv').config();
  ```

### 3. **Secure the Server**

* Never keep port `3000` open to the world long term
* Consider using **Nginx** as a reverse proxy and **SSL**

### 4. **Better Error Handling**

* Log full error for devs
* Show user-friendly message on frontend

---

Let me know if you want a zip-ready version of this project or want help packaging/deploying this in a more production-friendly way (e.g. Docker, ECS, etc).
