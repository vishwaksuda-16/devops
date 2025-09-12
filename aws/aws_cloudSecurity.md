# AWS Basics: Security, Cloud Types, Monitoring, IAM, MFA

## 1. Cloud Security
- **Definition**: Practices, technologies, and policies to protect cloud data, apps, and infrastructure.
- **Key Points**:
  - Shared Responsibility Model:  
    - AWS secures the **cloud** (infra, hardware).  
    - You secure things **in the cloud** (data, access, configs).  
  - Use IAM, encryption, monitoring, and MFA.

---

## 2. Cloud Deployment Models
1. **Public Cloud**  
   - Owned & operated by cloud providers (AWS, Azure, GCP).  
   - Resources shared among users.  
   - Example: Hosting a website on AWS.

2. **Private Cloud**  
   - Dedicated cloud environment for one organization.  
   - More control & security.  
   - Example: On-premises OpenStack cloud.

3. **Hybrid Cloud**  
   - Combination of public + private.  
   - Data/apps move between both.  
   - Example: Sensitive data in private, scalable apps in public.

---

## 3. CloudWatch
- **Definition**: Monitoring & observability service.  
- **Use**: Tracks metrics, logs, alarms, dashboards.  
- Example: Monitor CPU utilization of EC2.

---

## 4. CloudTrail
- **Definition**: Records **API calls & activities** in your AWS account.  
- **Use**: Auditing, compliance, troubleshooting.  
- Example: Track who terminated an EC2 instance.

---

## 5. AWS IAM (Identity and Access Management)
- **Definition**: Securely manage access to AWS resources.

### IAM Components:
- **Users** → Individual accounts (person/app).  
- **Groups** → Collection of users with same permissions.  
- **Roles** → Temporary permissions assigned to services/users.  
- **Policies** → JSON docs defining permissions (Allow/Deny).

✅ Example:  
- User "Alice" in group "Developers".  
- Group has policy → `AmazonS3ReadOnlyAccess`.  
- Alice can read S3 buckets but not delete.

---

## 6. MFA (Multi-Factor Authentication)
- **Definition**: Adds an extra layer of security (something you know + something you have).  
- AWS supports **virtual MFA** (Google Authenticator, Authy).

### Steps for Virtual MFA (Google Authenticator)
1. Login to AWS Management Console.  
2. Go to **IAM → Users → Security Credentials**.  
3. Click **Assign MFA Device**.  
4. Choose **Virtual MFA device**.  
5. Open **Google Authenticator app** → Scan QR code.  
6. Enter 2 consecutive codes → Confirm.  
7. Now login requires password + OTP from app.  

---

✨ **Tip to Remember**
- **Cloud Security** = Protect data & infra.  
- **Public / Private / Hybrid** = Ownership & usage model.  
- **CloudWatch** = Monitoring.  
- **CloudTrail** = Logging & auditing.  
- **IAM** = Who can do what.  
- **MFA** = Extra protection with OTP.
