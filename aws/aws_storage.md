# AWS Storage Services - Beginner's Guide

## 🗄️ AWS Storage Types Overview

### **Block Storage**
- **EBS (Elastic Block Store)**: Virtual hard drives for EC2 instances
- **EFS (Elastic File System)**: Shared file storage across multiple instances

### **Object Storage**
- **S3 (Simple Storage Service)**: Store files, images, videos, backups

### **Hybrid Storage**
- **Storage Gateway**: Connect on-premises to AWS storage

### **Data Migration**
- **Snowball**: Physical device to transfer large data (petabytes)
- **Snowmobile**: Truck-sized device for exabyte-scale transfers
- **Glacier**: Long-term archival storage

---

## 📦 Amazon S3 (Simple Storage Service)

### **What is S3?**
Think of S3 as Google Drive but for businesses - unlimited cloud storage for any type of file.

### **Key Features & Advantages**
- ✅ **99.999999999% (11 9's) durability** - Your data won't be lost
- ✅ **Unlimited storage** - Store as much as you want
- ✅ **Pay-as-you-use** - Only pay for what you store
- ✅ **Global accessibility** - Access from anywhere
- ✅ **Automatic backup** across multiple locations

---

## 🪣 Buckets & Objects

### **Buckets**
- Container for your files (like folders)
- Must have **globally unique names**
- Created in specific **regions**

### **Objects**
- The actual files you store
- Can be 0 bytes to 5TB in size
- Each object has a unique **key** (filename + path)

**Example:**
```
Bucket: my-company-photos
Object: vacation-pics/beach.jpg
```

---

## 🔄 Versioning

### **What is Versioning?**
Keeps multiple versions of the same file when you update it.

### **Benefits:**
- 🛡️ **Protect against accidental deletion**
- 🛡️ **Protect against corruption**
- 📚 **Keep history of changes**

**Example:**
```
document.pdf (Version 1)
document.pdf (Version 2) ← Current
document.pdf (Version 3) ← Latest
```

---

## 🌍 Regions & Cross Region Replication

### **What are Regions?**
Physical locations where AWS has data centers (like US-East, Europe, Asia)

### **Cross Region Replication (CRR)**
Automatically copy your data to another region for:
- 🌐 **Disaster recovery**
- 🚀 **Faster access globally**
- 📋 **Compliance requirements**

---

## ⚡ Faster Data Transfer

### **AWS CloudFront**
- **What**: Content Delivery Network (CDN)
- **How**: Stores copies of your content at **Edge Locations** worldwide
- **Benefit**: Users get content from nearest location = faster loading

### **Edge Locations**
- 400+ locations globally
- Closer to users than main AWS regions
- Cache frequently accessed content

### **S3 Transfer Acceleration**
- Uses CloudFront's edge locations for faster uploads
- Can improve upload speeds by 50-500%

---

## 💾 S3 Storage Classes

### **Standard**
- 🏃‍♂️ **Frequent access**
- 💰 **Higher cost**
- ⚡ **Instant retrieval**

### **Standard-Infrequent Access (IA)**
- 📅 **Monthly access**
- 💸 **Lower storage cost**
- 💰 **Retrieval fee applies**

### **Glacier**
- 🗄️ **Archive/backup**
- 💸 **Cheapest storage**
- ⏰ **Minutes to hours retrieval**

### **Glacier Deep Archive**
- 🏛️ **Long-term archive**
- 💸 **Lowest cost**
- ⏰ **12+ hours retrieval**

---

## 🔒 Security & Access Control

### **Bucket Policies**
JSON documents that define who can access your bucket and what they can do.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow", //or Deny
      "Principal": "*",
      "Action": "s3:GetObject", //different actions - get,delete,create etc
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

### **AWS Policy Generator**
- Web-based tool to create policies
- No need to write JSON manually
- Point-and-click interface

### **ACL (Access Control Lists)**
- Simpler way to control access
- Good for basic permissions
- Grant access to AWS accounts or groups

---

## ♻️ Lifecycle Management

### **Transition Rules**
Automatically move objects between storage classes to save money:

```
Day 0-30: Standard
Day 30-90: Standard-IA
Day 90+: Glacier
```

### **Expiration Rules**
Automatically delete objects after specified time:
- Delete old log files after 1 year
- Remove temporary files after 30 days

---

## 🎬 Real-World Use Case: IMDb

### **The Challenge**
IMDb needed ultra-fast movie/celebrity search with low latency.

### **The Solution**
1. **Pre-calculate all searches**: Create documents for every possible letter combination (23 × 1,030 combinations for 20 characters)

2. **Store in S3**: All pre-calculated documents stored in Amazon S3

3. **Distribute globally**: Use **CloudFront** to push documents to edge locations worldwide

4. **Reduce search space**: Leverage IMDb's authority to narrow down to ~150,000 relevant documents

5. **Fast distribution**: S3 + CloudFront can distribute all documents globally in just **a few hours**

### **Result**
⚡ Lightning-fast search results with minimal latency worldwide!

---

## 📝 Key Takeaways

1. **S3** = Unlimited, durable cloud storage
2. **Versioning** = Protection against data loss
3. **Regions** = Choose location for compliance/performance
4. **CloudFront** = Global content delivery for speed
5. **Storage Classes** = Match usage patterns to costs
6. **Lifecycle** = Automatic cost optimization
7. **Security** = Multiple layers of access control
