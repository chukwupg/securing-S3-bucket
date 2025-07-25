# Securing Your First S3 Bucket & IAM User

## 📌 Overview
This project is part of my **#100DaysOfCybersecurity Challenge (Day 9)**.  
The goal is to understand how **misconfigured S3 buckets** and **overly permissive IAM policies** can lead to security issues — and how to fix them following the **principle of least privilege**.

---

## 🎯 Objectives

✅ Simulate a public S3 bucket misconfiguration  
✅ Create an IAM user (`junior-analyst`) with controlled access  
✅ Fix the misconfiguration using a secure bucket policy  
✅ Enable S3 server access logging for auditing  

---

## 🛠 Tools Used

- **AWS Management Console**  
- **IAM & S3**  
- **AWS CLI** 

---

## 📝 Steps & Screenshots

### **1. Create S3 Buckets**
- **Bucket Name:** `bonkina-bucket` (contains file and folder)
- **Bucket Name:** `server-logstash` (for server logs)
<img width="859" height="528" alt="Screenshot 2025-07-25 070419" src="https://github.com/user-attachments/assets/07273515-217a-40cf-8816-f7a107cda243" />


---

### **2. Upload a Sample File**
- **File:** `anon_sensitive.txt`  
<img width="858" height="492" alt="Screenshot 2025-07-25 193421" src="https://github.com/user-attachments/assets/9d59dae6-f865-4d95-9388-90a881504dd8" />


---

### **3. Simulate Misconfiguration**
- **Disabled Block Public Access**  
- **Made the object public and accessed via its URL**  
<img width="935" height="835" alt="Screenshot 2025-07-25 021426" src="https://github.com/user-attachments/assets/2ac07901-8ac5-4479-bddb-d17ac7ddad50" />
<img width="634" height="282" alt="Screenshot 2025-07-24 190126" src="https://github.com/user-attachments/assets/c1d4022c-2fea-4124-b5ed-70fe9bfc4a3e" />



---

### **4. Create an IAM User**
- **Name:** `junior-analyst`  
- **Attached Policy:** AmazonS3FullAccess *(initially, for testing)*  
<img width="777" height="633" alt="Screenshot 2025-07-24 191508" src="https://github.com/user-attachments/assets/7f5f41e8-2027-49fd-b16b-e6fd41d7d91c" />


---

### **5. Fix the Misconfiguration**

#### **a) Remove Public Access**
- **Re-enabled Block Public Access settings**  
#### **b) Apply a Bucket Policy (Restrict to IAM User Only)**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<ACCOUNT_ID>:user/junior-analyst"
      },
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::your-name-cloudsec-demo",
        "arn:aws:s3:::your-name-cloudsec-demo/*"
      ]
    }
  ]
}
```
<img width="1132" height="1188" alt="Screenshot 2025-07-25 051258" src="https://github.com/user-attachments/assets/77781372-4c25-49be-be6c-e9020007b518" />

---

### **6. Enable S3 Server Access Logging**
- **Logging Target Bucket Configured**  
<img width="743" height="341" alt="Screenshot 2025-07-25 062355" src="https://github.com/user-attachments/assets/5b42d65c-9775-4521-985f-0a3df10d7eca" />


---

## ✅ **Verification**

- **Public Access Test:**  
  The public URL now returns an `AccessDenied` error.
  <img width="854" height="327" alt="Screenshot 2025-07-25 201711" src="https://github.com/user-attachments/assets/488ecb06-de9f-446a-b77b-ef929c46a074" />


- **IAM User Test:**  
  - Logged in as `junior-analyst` → Successfully listed & downloaded files.  
  - Logged in as another user account → **Access denied.**

---

## 📖 **Key Learnings**

- **Never leave S3 buckets publicly accessible** unless strictly necessary.  
- Always apply the **principle of least privilege** when assigning IAM roles.  
- **Enable server access logging** for monitoring & auditing.  

---

## 🔗 **Next Steps**

- Automate this setup using **Terraform** or **CloudFormation**.  
- Explore more **AWS misconfiguration scenarios**.

---

## ✍ **Author**

👩‍💻 **Chukwu PraiseGod**  
Follow my journey: [X](https://x.com/chukwupg) | [LinkedIn](https://linkedin.com/in/chukwupg)  
