# AWS Compute Services - Beginner Guide

## What is an Instance?

An **instance** is simply a virtual computer in the cloud. Think of it like renting a computer that you can access from anywhere. It has:
- CPU (processor)
- Memory (RAM)
- Storage space
- Network connection

## What is Amazon EC2?

**EC2 (Elastic Compute Cloud)** is Amazon's service for creating virtual computers. You can:
- Start and stop them anytime
- Choose how powerful they are
- Pay only for what you use
- Access them from anywhere

## Types of EC2 Instances

### General Purpose (T3, M5)
- Balanced performance
- Good for websites and small applications

### Compute Optimized (C5)
- Fast processors
- Good for applications that need lots of computing power

### Memory Optimized (R5)
- Lots of RAM
- Good for databases and data processing

### Storage Optimized (I3)
- Fast storage
- Good for applications that read/write lots of data

### GPU Optimised 
- For graphic intensive resources
- Example : 3D Modeling   

## EC2 Use Cases

- **Web Applications**: Host websites
- **Development**: Create test environments
- **Databases**: Run database servers
- **Big Data**: Process large amounts of data

## What is AWS Lambda?

**Lambda** is serverless computing - you just upload your code and AWS runs it for you. No need to manage servers!

### Key Benefits:
- No server management
- Pay only when code runs
- Automatically scales
- Very fast to deploy

### Example Lambda Function:
```python
def lambda_handler(event, context):
    name = event.get('name', 'World')
    return f'Hello, {name}!'
```

## AWS Compute Domains

### Serverless
- **Lambda**: Run code without servers

### Virtual Machines
- **EC2**: Traditional virtual servers

### Platform Services
- **Elastic Beanstalk**: Easy app deployment

### Containers
- **ECS/EKS**: Run containerized applications

## AWS SDKs

SDKs are tools that let you control AWS from your code:
- **Python**: Boto3
- **JavaScript**: AWS SDK for JS
- **Java**: AWS SDK for Java
- Available for most programming languages

## Why Use AWS Lambda?

- **Cost**: Only pay when it runs
- **Simple**: No servers to manage
- **Fast**: Starts in milliseconds
- **Scalable**: Handles any amount of traffic

## Lambda Demo

### Simple Function:
import json

def lambda_handler(event, context):
    # Get name from input
    name = event.get('name', 'World')
    age = event.get('age', 'unknown')
    
    # Create response message
    message = f"Hello {name}! Your age is {age}."
    
    return {
        'statusCode': 200,
        'body': json.dumps({
            'message': message,
            'input_received': event
        })
    }

    Sample Input:
    json{
        "name": "John",
        "age": 25
    }
    Sample Output:
    json{
        "statusCode": 200,
        "body": "{\"message\": \"Hello John! Your age is 25.\", \"input_received\": {\"name\": \"John\", \"age\": 25}}"
    }

### Steps to Deploy:
1. Go to AWS Lambda console
2. Click "Create function"
3. Paste your code
4. Click "Deploy"
5. Test it!

## What is AWS Elastic Beanstalk?

**Elastic Beanstalk** is like a simple way to put your web application online. You just:
1. Upload your code
2. AWS handles everything else (servers, scaling, monitoring)


## What is PaaS?

**Platform as a Service** means you focus on your code, and the platform handles:
- Servers
- Scaling
- Updates
- Monitoring

Elastic Beanstalk is AWS's PaaS offering.

## Elastic Beanstalk Features

- **Easy Deployment**: Just upload your code
- **Auto Scaling**: Handles traffic spikes automatically
- **Health Monitoring**: Tells you if something is wrong
- **Version Control**: Easy to rollback changes
- **Free**: You only pay for the underlying resources

## Beanstalk Architecture

```
Your Code → Beanstalk → Load Balancer → Multiple Servers
```

Beanstalk automatically creates:
- Load balancer (distributes traffic)
- Multiple servers (for reliability)
- Auto scaling (adds/removes servers as needed)

## How to Deploy in Beanstalk

### Method 1: Web Console
1. Go to Elastic Beanstalk console
2. Click "Create Application"
3. Choose your platform (Python, Java, etc.)
4. Upload your code (ZIP file)
5. Click "Create Environment"
6. Wait 5-10 minutes - done!

### Method 2: Command Line
```bash
# Install EB CLI
pip install awsebcli

# Initialize
eb init

# Deploy
eb create my-app

# Open in browser
eb open
```

## Web Server vs Worker Server

### Web Server
- **Purpose**: Serves websites to users
- **How it works**: Responds to web requests immediately
- **Example**: Your website's homepage

### Worker Server
- **Purpose**: Does background tasks
- **How it works**: Processes jobs from a queue
- **Example**: Sending emails, processing images

### When to Use Each:
- **Web Server**: When users need immediate responses
- **Worker Server**: When tasks take a long time or happen in background

### Simple Example:
```
User uploads photo → Web Server (quick response) → Worker Server (resize photo)
```

## Summary

- **EC2**: Virtual computers you manage
- **Lambda**: Code that runs without servers
- **Beanstalk**: Easy way to deploy web apps
- **Web Servers**: Handle user requests
- **Worker Servers**: Handle background tasks

Choose based on your needs:
- Simple web app → Beanstalk
- Custom setup → EC2  
- Small functions → Lambda