# Section 4 – IAM / AWS CLI
[**Table of Contents**](#section-4--iam--aws-cli)  
- [4.11: IAM Users / Groups](#411-iam-users--groups)  
- [4.14: IAM Policies Structure](#414-iam-policies-structure)  
- [4.16: IAM Protection / Defense](#416-iam-protection--defense)  
- [4.18: Keys, CLI, and SDK](#418-keys-cli-and-sdk)  
- [4.25: IAM Roles](#425-iam-roles)  
- [4.27: IAM Security Tools](#427-iam-security-tools)  
- [4.29: IAM Best Practices](#429-iam-best-practices)

---

## 4.11: IAM Users / Groups
- **IAM (Identity and Access Management)** is **Global**  
- We create **users** and **groups** in IAM  
- A **user** can belong to **multiple groups**  
- Each group defines its own **privileges**  
- Always follow the **Principle of Least Privilege** for security  

---

## 4.14: IAM Policies Structure
- IAM policies are JSON documents with:  
  - **Version** – policy language version (e.g., `"2012-10-17"`)  
  - **Id** – identifier for the policy *(optional)*  
  - **Statement** – main policy content, consisting of:  
    - **Sid** – statement ID *(optional)*  
    - **Effect** – `Allow` or `Deny`  
    - **Principal** – the account, user, or role the policy applies to  
    - **Action** – list of allowed/denied API actions  
    - **Resource** – list of resources affected (e.g., an S3 bucket ARN)  
    - **Condition** – conditions when the policy is active *(optional)*  

**Example Structure:**

    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "ExampleStatement",
          "Effect": "Allow",
          "Principal": {"AWS": "arn:aws:iam::123456789012:user/ExampleUser"},
          "Action": "s3:*",
          "Resource": "arn:aws:s3:::example-bucket/*"
        }
      ]
    }

---

## 4.16: IAM Protection / Defense
- **Password Policy** options:  
  - Set **minimum length**  
  - Require **specific character types**  
  - Allow IAM users to **change their own passwords**  
  - **Expire** passwords after a set time  
  - **Prevent password reuse**  

- **MFA (Multi-Factor Authentication)** combines:  
  - Something you **know** (password)  
  - Something you **have** (security device)  

**MFA Options:**
1. **Virtual MFA Device** – Google Authenticator, Authy *(mobile only)*  
2. **U2F Security Key** – Physical key like **YubiKey**  
3. **Hardware Key Fob MFA Device** – e.g. **Gemalto**  
4. **Hardware MFA for AWS GovCloud** – e.g. **SurePassID**

---

## 4.18: Keys, CLI, and SDK
**Three ways to access AWS:**
1. **Management Console** – via password + MFA  
2. **CLI** – via **Access Keys**  
3. **SDK** – via **Access Keys**

**Access Keys:**
- Generated through the AWS Console  
- **Access Key ID** ≈ username  
- **Secret Access Key** ≈ password  

---

## 4.25: IAM Roles
- IAM **Roles** are like users but used by **AWS services**, not people  
- Example:  
  - An **EC2 instance** assumes a role to access other AWS services  
  - It can only perform actions allowed by that role’s policies  

---

## 4.27: IAM Security Tools
- **IAM Credentials Report (account-level):**  
  - Lists all users and credential status (passwords, access keys, MFA)  
- **IAM Access Advisor (user-level):**  
  - Shows services a user can access and **last-used timestamps**  
  - Helps enforce **least privilege** principle  

---

## 4.29: IAM Best Practices
✅ Don’t use the **root account** except for initial setup  
✅ **One physical person = one IAM user**  
✅ Assign users to **groups**, and attach permissions to groups  
✅ Create a **strong password policy**  
✅ **Enforce MFA**  
✅ Use **roles** for AWS service permissions  
✅ Use **Access Keys** for programmatic (CLI/SDK) access  
✅ **Audit permissions** using Credentials Report & Access Advisor  
🚫 **Never share IAM users or Access Keys**

---
