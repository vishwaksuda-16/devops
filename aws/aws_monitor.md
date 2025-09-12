# AWS CloudWatch - Monitoring & Management Guide

## 📊 AWS Monitoring & Management

### **What is AWS Monitoring?**
Think of monitoring as having **security cameras and sensors** throughout your house to know what's happening at all times.

### **Why Do We Need Monitoring?**
- 👀 **See what's happening** with your AWS resources
- 🚨 **Get alerts** when something goes wrong
- 📈 **Track performance** over time
- 💰 **Optimize costs** by understanding usage
- 🔧 **Troubleshoot issues** quickly

---

## ☁️ AWS CloudWatch

### **What is CloudWatch?**
CloudWatch is AWS's **"security system"** that watches over all your AWS resources 24/7 and tells you what's happening.

### **Simple Analogy:**
```
CloudWatch = Security guard with cameras
Your AWS resources = Different rooms in building
Metrics = Reports from each room
Alarms = Alert system when something's wrong
```

---

## 📈 Types of Monitoring

### **Basic Monitoring (FREE)**
- 📊 **5-minute intervals** - Data every 5 minutes
- 🆓 **Free tier included**
- ✅ **Basic metrics** like CPU, Network, Disk

### **Detailed Monitoring (PAID)**
- ⚡ **1-minute intervals** - Data every minute
- 💰 **Extra cost** but more precise
- 🔍 **Faster problem detection**

**Example:**
```
Basic: CPU at 10:00, 10:05, 10:10 (every 5 min)
Detailed: CPU at 10:00, 10:01, 10:02 (every 1 min)
```

---

## 🛠️ What Does CloudWatch Do?

### **Core Functions:**
1. 📊 **Collect Metrics** - Gather performance data
2. 📝 **Store Logs** - Keep application and system logs
3. 🚨 **Create Alarms** - Alert when thresholds are crossed
4. 📈 **Visualize Data** - Create dashboards and graphs
5. 🤖 **Trigger Actions** - Automatically respond to events

---

## 🎯 AWS Resources Monitored by CloudWatch

### **Compute Services:**
- 🖥️ **EC2**: CPU, Memory, Network, Disk
- ⚡ **Lambda**: Invocations, Duration, Errors
- 🚢 **ECS**: Container metrics

### **Storage Services:**
- 🗄️ **S3**: Bucket size, Requests, Errors
- 💾 **EBS**: Volume read/write, IOPS

### **Database Services:**
- 🗃️ **RDS**: CPU, Memory, Connections
- ⚡ **DynamoDB**: Read/Write capacity, Throttles

### **Network Services:**
- 🌐 **ELB**: Request count, Latency, Errors
- 🚀 **CloudFront**: Cache hits, Origin requests

---

## 📊 CloudWatch Core Concepts

### **1. Metrics**
**What**: Numerical data points about your resources
```
Examples:
- CPUUtilization: 75%
- NetworkIn: 1000 bytes
- DiskReadOps: 50 operations
```

### **2. Dimensions**
**What**: Categories that identify metrics
```
Examples:
- InstanceId: i-1234567890abcdef
- LoadBalancerName: my-load-balancer
- BucketName: my-s3-bucket
```

### **3. Statistics**
**What**: Mathematical calculations over time periods
- 📊 **Average**: Mean value
- 📈 **Maximum**: Highest value
- 📉 **Minimum**: Lowest value
- 📋 **Sum**: Total of all values
- 🔢 **SampleCount**: Number of data points

### **4. Alarms**
**What**: Notifications when metrics cross thresholds
```
Example Alarm:
"Alert me when CPU > 80% for 2 consecutive periods"
```

---

## ⚙️ How CloudWatch Works

### **Data Flow:**
```
AWS Resources → Generate Metrics → CloudWatch Collects → 
Store in CloudWatch → Create Alarms → Trigger Actions
```

### **Step-by-Step Process:**
1. **📡 Collection**: AWS services automatically send metrics
2. **💾 Storage**: CloudWatch stores metrics for 15 months
3. **📊 Visualization**: View data in graphs and dashboards  
4. **🚨 Monitoring**: Set alarms on metric thresholds
5. **🤖 Actions**: Trigger responses (emails, auto-scaling, etc.)

---

## 🎯 CloudWatch Events, Rules & Targets

### **CloudWatch Events (Now EventBridge)**
**What**: Responds to changes in AWS resources in real-time

### **Events**
**What**: Something happening in AWS
```
Examples:
- EC2 instance state change (running → stopped)
- S3 object uploaded
- Lambda function completed
```

### **Rules**
**What**: Conditions that match events
```
Example Rule:
"When any EC2 instance changes state"
"Every day at 9 AM"
"When CPU > 90%"
```

### **Targets**
**What**: Where to send matched events
```
Common Targets:
- 📧 SNS (email notifications)
- ⚡ Lambda functions
- 📋 SQS queues
- 🔧 EC2 actions (start/stop)
```

### **Event Flow:**
```
Event Occurs → Rule Matches → Target Executes Action
```

---

## 📝 CloudWatch Logs

### **What are CloudWatch Logs?**
Central place to store, monitor, and access log files from AWS resources and applications.

### **Key Concepts:**

#### **Log Events**
**What**: Individual log entries with timestamp and message
```
Example:
[2024-01-15 10:30:45] ERROR: Database connection failed
```

#### **Log Streams**
**What**: Sequence of log events from same source
```
Example:
- web-server-1.log
- web-server-2.log  
- database-error.log
```

#### **Log Groups**
**What**: Collection of log streams with same settings
```
Example Log Group: /aws/lambda/my-function
Contains streams from different function executions
```

### **Log Management:**

#### **Log Retention**
**What**: How long to keep logs before deletion
```
Options:
- 1 day to 10 years
- Never expire (costs more)
- Default: Never expire
```

#### **Log Storage**
**What**: Where logs are physically stored
- 📊 **CloudWatch Logs**: Real-time monitoring
- 🗄️ **S3**: Long-term archival (cheaper)
- ❄️ **Glacier**: Very long-term (cheapest)

#### **DNS Queries Logging**
**What**: Track Route 53 DNS query logs
```
Log Format:
timestamp query-name query-type response-code
```

---

## 🚀 Demo: Auto Start/Stop EC2 with CloudWatch

### **What We'll Build:**
Automatically start/stop EC2 instances based on CPU utilization with email notifications.

### **Architecture:**
```
CloudWatch Metrics → Alarms → Lambda Function → EC2 Action → SNS Email
```

### **Prerequisites:**
✅ AWS Account  
✅ EC2 instance running  
✅ Email address for notifications

---

### **Step 1: Create SNS Topic for Email Notifications**

#### **1.1 Create SNS Topic**
```bash
1. Go to SNS service
2. Click "Create topic"
3. Type: Standard
4. Name: ec2-auto-management
5. Click "Create topic"
```

#### **1.2 Create Email Subscription**
```bash
1. Click "Create subscription"
2. Protocol: Email
3. Endpoint: your-email@example.com
4. Click "Create subscription"
5. Check email and confirm subscription
```

---

### **Step 2: Create Lambda Function for EC2 Control**

#### **2.1 Create Lambda Function**
```bash
1. Go to Lambda service
2. Click "Create function"
3. Author from scratch
4. Function name: ec2-auto-manager
5. Runtime: Python 3.9
6. Click "Create function"
```

#### **2.2 Lambda Function Code**
```python
import json
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2')
    sns = boto3.client('sns')
    
    # Get instance ID from CloudWatch alarm
    instance_id = event['instance_id']
    action = event['action']  # 'start' or 'stop'
    
    try:
        if action == 'stop':
            ec2.stop_instances(InstanceIds=[instance_id])
            message = f"EC2 instance {instance_id} stopped due to low CPU usage"
        elif action == 'start':
            ec2.start_instances(InstanceIds=[instance_id])
            message = f"EC2 instance {instance_id} started due to high CPU usage"
        
        # Send SNS notification
        sns.publish(
            TopicArn='arn:aws:sns:us-east-1:123456789012:ec2-auto-management',
            Message=message,
            Subject='EC2 Auto Management Alert'
        )
        
        return {
            'statusCode': 200,
            'body': json.dumps(f'Successfully {action}ed instance {instance_id}')
        }
        
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps(f'Error: {str(e)}')
        }
```

#### **2.3 Configure Lambda Permissions**
```bash
1. Go to "Configuration" tab
2. Click "Permissions"
3. Click on execution role name
4. Add these policies:
   - AmazonEC2FullAccess
   - AmazonSNSFullAccess
```

---

### **Step 3: Create CloudWatch Alarms**

#### **3.1 High CPU Alarm (Start Instance)**
```bash
1. Go to CloudWatch service
2. Click "Alarms" → "Create alarm"
3. Click "Select metric"
4. Choose: EC2 → Per-Instance Metrics
5. Select your instance → CPUUtilization
6. Click "Select metric"
```

**Alarm Configuration:**
```bash
Conditions:
- Threshold type: Static
- Whenever CPUUtilization is: Greater than 80
- For: 2 consecutive periods of 5 minutes

Actions:
- Alarm state trigger: In alarm
- Send notification to: ec2-auto-management
- Lambda function: ec2-auto-manager

Additional Settings:
- Alarm name: high-cpu-start-instance
- Description: Start instance when CPU > 80%
```

#### **3.2 Low CPU Alarm (Stop Instance)**
```bash
Follow same steps as above but:

Conditions:
- Whenever CPUUtilization is: Lower than 10
- For: 10 consecutive periods of 5 minutes

Additional Settings:
- Alarm name: low-cpu-stop-instance
- Description: Stop instance when CPU < 10% for 50 minutes
```

---

### **Step 4: Test the Setup**

#### **4.1 Test High CPU (Start Instance)**
```bash
1. Stop your EC2 instance manually
2. SSH to instance and run:
   stress --cpu 2 --timeout 600s  # Generate CPU load
3. Wait 10-15 minutes
4. Check if instance starts automatically
5. Check email for notification
```

#### **4.2 Test Low CPU (Stop Instance)**
```bash
1. Let instance run idle (no CPU load)
2. Wait 50+ minutes
3. Check if instance stops automatically  
4. Check email for notification
```

#### **4.3 Monitor in CloudWatch**
```bash
1. Go to CloudWatch → Alarms
2. Watch alarm states change:
   - OK → In Alarm (triggers action)
   - In Alarm → OK (normal operation)
```

---

### **Step 5: View Logs and Metrics**

#### **5.1 Lambda Logs**
```bash
1. Go to Lambda → ec2-auto-manager
2. Click "Monitor" tab
3. Click "View logs in CloudWatch"
4. See execution logs and any errors
```

#### **5.2 CloudWatch Dashboard**
```bash
1. Go to CloudWatch → Dashboards
2. Click "Create dashboard"
3. Add widgets for:
   - EC2 CPU Utilization
   - Lambda Invocations  
   - SNS Published Messages
```

---

## 📊 Cost Optimization Tips

### **CloudWatch Costs:**
- 📊 **Metrics**: First 10 metrics free, then $0.30/metric/month
- 🚨 **Alarms**: First 10 free, then $0.10/alarm/month  
- 📝 **Logs**: $0.50/GB ingested, $0.03/GB stored/month

### **Cost Saving Tips:**
1. 🗑️ **Delete unused alarms** and log groups
2. ⏰ **Set log retention periods** (don't keep forever)
3. 📊 **Use basic monitoring** unless you need detailed
4. 🎯 **Filter logs** to reduce storage costs

---

## ✅ Key Takeaways

1. **CloudWatch** = AWS monitoring and logging service
2. **Metrics** = Performance data from AWS resources  
3. **Alarms** = Automated alerts and actions
4. **Logs** = Centralized log storage and analysis
5. **Events** = Real-time response to AWS changes
6. **Auto-scaling** = Respond automatically to load changes

**Start Simple:** Begin with basic monitoring, add alarms for critical resources, then build automation as you grow!

---

## 🔗 Quick Reference

### **Common Metrics to Monitor:**
- 🖥️ **EC2**: CPUUtilization, NetworkIn/Out
- 🗃️ **RDS**: DatabaseConnections, CPUUtilization  
- 🚀 **Lambda**: Duration, Errors, Throttles
- ⚖️ **ELB**: RequestCount, TargetResponseTime

### **Alarm Best Practices:**
- 📊 Set reasonable thresholds (not too sensitive)
- ⏱️ Use multiple periods to avoid false alarms
- 📧 Don't spam notifications - group related alarms
- 🧪 Test alarms in non-production first