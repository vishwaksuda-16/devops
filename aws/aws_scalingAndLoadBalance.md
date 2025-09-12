# AWS Basics: Snapshots, AMIs, Auto Scaling & Load Balancers

## 1. Snapshots
- **Definition**: A backup of your EBS (Elastic Block Store) volume at a point in time.
- **Use case**: Disaster recovery, creating new volumes from existing data.

✅ **Key Points**
- Stored in S3 (managed by AWS).
- Can be used to create new EBS volumes in the same or different region.
- Incremental → only changed blocks are saved.

---

## 2. AMIs (Amazon Machine Images)
- **Definition**: A template that contains the software configuration (OS, applications, settings).
- **Use case**: Launching new EC2 instances quickly with pre-installed setup.

✅ **Key Points**
- Types:  
  - **Public AMIs** → Provided by AWS or community.  
  - **Custom AMIs** → Created from your own instance.  
- You can launch multiple instances from one AMI.

---

## 3. Auto Scaling
- **Definition**: Automatically adds/removes EC2 instances based on demand.
- **Use case**: Saves cost, ensures performance under varying loads.

✅ **Key Points**
- Uses **Auto Scaling Groups (ASG)**.
- Policies define when to scale (e.g., CPU > 70% → add an instance).
- Ensures **high availability** & **cost optimization**.

---

## 4. Load Balancers
- **Definition**: Distributes incoming traffic across multiple EC2 instances.
- **Use case**: Avoids overload on a single server, improves fault tolerance.

### Types:
1. **Classic Load Balancer (CLB)**  
   - Old generation.  
   - Works at Layer 4 (TCP) & Layer 7 (HTTP/HTTPS).  

2. **Application Load Balancer (ALB)**  
   - Newer, advanced.  
   - Works only at Layer 7 (HTTP/HTTPS).  
   - Supports routing rules (e.g., /api → one group, /app → another).

---

## 5. Demo (Steps Only)

### Create AMI & Snapshot
1. Launch an EC2 instance.  
2. Install required software.  
3. From **EC2 Dashboard** → Actions → Create Image (AMI).  
4. From **Volumes** → Create Snapshot.  

### Auto Scaling
1. Create a **Launch Template** (choose AMI, instance type).  
2. Create an **Auto Scaling Group** (attach template, choose subnets).  
3. Define scaling policies (e.g., target CPU).  
4. Attach a **Load Balancer** for traffic distribution.  

### Load Balancer
1. Go to **EC2 → Load Balancers → Create Load Balancer**.  
2. Choose **Application Load Balancer**.  
3. Select VPC, subnets, and security groups.  
4. Register EC2 instances (targets).  
5. Test using the ALB DNS name.  

---

✨ **Tip to Remember**
- **Snapshots** = Backup of volumes  
- **AMI** = Template to launch EC2  
- **Auto Scaling** = Scale in/out automatically  
- **Load Balancer** = Distributes traffic
