
🔐 Restricting Amazon EC2 Access to the Paris Region (eu-west-3) Using IAM

## 📌 Overview

This project demonstrates how to **restrict Amazon EC2 access to a single AWS region (Paris – eu-west-3)** using an IAM policy.
The policy **allows full EC2 access only in Paris** and **explicitly denies EC2 actions in all other regions**, ensuring strong region-level governance and compliance.

---

## 🎯 Objective

* Allow **full Amazon EC2 access** only in **eu-west-3 (Paris)**
* Deny **all EC2 actions** in **every other AWS region**
* Enforce access control using **IAM condition keys**
* Validate the policy behavior through real testing

---

## 🧩 AWS Services Used

* **IAM (Identity and Access Management)** – Policy creation and user permissions
* **Amazon EC2** – Service access control and validation

---

## 📜 IAM Policy Logic

The policy uses the condition key `aws:RequestedRegion` with:

* `StringEquals` → to **allow** EC2 access in Paris
* `StringNotEquals` → to **deny** EC2 access in all other regions

### IAM Policy (JSON)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowEC2OnlyInParisRegion",
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "aws:RequestedRegion": "eu-west-3"
        }
      }
    },
    {
      "Sid": "DenyEC2InAllOtherRegions",
      "Effect": "Deny",
      "Action": "ec2:*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestedRegion": "eu-west-3"
        }
      }
    }
  ]
}
```

---

## 🛠 Implementation Summary

* Created a **customer-managed IAM policy**
* Added **two policy statements**:

  * Allow EC2 actions only in Paris
  * Explicitly deny EC2 actions outside Paris
* Attached the policy directly to an **IAM user**
* Verified behavior using the AWS Management Console

---

## ✅ Validation & Testing

| Region              | Action     | Result                           |
| ------------------- | ---------- | -------------------------------- |
| Mumbai (ap-south-1) | Launch EC2 | ❌ Access Denied                  |
| Paris (eu-west-3)   | Launch EC2 | ✅ Instance launched successfully |

Screenshots in the document confirm:

* Permission denied error in non-Paris regions
* Successful EC2 instance creation in Paris 

---

## 🔒 Security Best Practices Demonstrated

* Principle of **least privilege**
* Use of **explicit deny** for enforcement
* Region-level access control using IAM conditions
* Safe even if additional EC2 permissions exist elsewhere

---

## 📂 Repository Structure (Suggested)

```
├── README.md
├── iam-policy.json
├── screenshots/
│   ├── deny-mumbai.png
│   └── allow-paris.png
└── documentation.pdf
```

---

## 🚀 Use Cases

* Region-based compliance enforcement
* Prevent accidental resource creation in wrong regions
* Enterprise IAM guardrails
* AWS security & governance projects

---

## 🧠 Key Takeaway

> **Explicit Deny + RequestedRegion condition = strong regional control in AWS IAM**
 
