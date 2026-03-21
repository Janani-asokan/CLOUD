Here’s a **complete, interview-focused, end-to-end guide to Amazon S3 (Simple Storage Service)** from basics → advanced. I’ll keep it clear, structured, and practical so you can both **learn and answer confidently in interviews**.

---

# 🌐 1. What is Amazon S3?

**Amazon S3 (Simple Storage Service)** is an object storage service by Amazon Web Services used to store and retrieve any amount of data from anywhere.

### 📌 Key Characteristics

* Unlimited storage
* Highly durable (11 9’s → 99.999999999%)
* Scalable and cost-effective
* Accessible via HTTP/HTTPS

### 🧠 Interview Answer (Short)

> S3 is a highly durable, scalable object storage service used for storing unstructured data like images, videos, logs, and backups.

---

# 🪣 2. Core Concepts (VERY IMPORTANT)

## 2.1 Bucket

* A **bucket** is a container for objects
* Must have **globally unique name**
* Created in a specific region

👉 Example:

```
my-company-logs-bucket
```

## 2.2 Object

* Actual data stored in S3
* Consists of:

  * Key (name)
  * Value (data)
  * Metadata
  * Version ID (if versioning enabled)

## 2.3 Key

* Unique identifier inside a bucket

```
images/profile.jpg
```

---

# 📦 3. Storage Classes (VERY COMMON INTERVIEW QUESTION)

| Storage Class           | Use Case                 |
| ----------------------- | ------------------------ |
| S3 Standard             | Frequently accessed data |
| S3 Intelligent-Tiering  | Unknown access patterns  |
| S3 Standard-IA          | Infrequent access        |
| S3 One Zone-IA          | Less critical data       |
| S3 Glacier              | Archival                 |
| S3 Glacier Deep Archive | Long-term archival       |

### 🧠 Interview Tip

> If cost optimization is asked → talk about lifecycle + storage classes.

---

# 🔐 4. Security in S3 (CRITICAL)

## 4.1 Bucket Policies

* JSON-based policies attached to bucket

## 4.2 IAM Policies

* Attached to users/roles

## 4.3 ACL (Access Control List)

* Legacy method (less used now)

## 4.4 Encryption Types

* SSE-S3 → AWS manages keys
* SSE-KMS → Uses KMS keys
* SSE-C → Customer provides keys

### 🧠 Interview Answer

> S3 security is controlled using IAM policies, bucket policies, and encryption like SSE-S3 or SSE-KMS.

---

# 🔄 5. Versioning

* Keeps multiple versions of an object
* Helps in:

  * Recovery from accidental deletes
  * Rollbacks

### States:

* Enabled
* Suspended

---

# 🗂️ 6. Lifecycle Policies

Automates object movement or deletion.

### Example:

* Move to Glacier after 30 days
* Delete after 365 days

### 🧠 Interview Answer

> Lifecycle policies optimize cost by automatically transitioning objects between storage classes.

---

# 🌍 7. S3 Data Consistency

* **Strong read-after-write consistency** (important update)

### Means:

* Immediately available after upload/update

---

# ⚡ 8. Performance & Optimization

## 8.1 Multipart Upload

* Upload large files in parts
* Improves speed & reliability

## 8.2 Transfer Acceleration

* Uses edge locations for faster upload

---

# 🌐 9. S3 Access Methods

* AWS Console
* CLI
* SDKs
* REST API

---

# 🌎 10. Static Website Hosting

* S3 can host static websites (HTML, CSS, JS)

### Requirements:

* Enable static hosting
* Public access
* Index + error file

---

# 🔗 11. Pre-Signed URLs

* Temporary access to private objects

### Use Case:

* Secure file download/upload without exposing bucket

---

# 📡 12. Event Notifications

Triggers actions when events happen:

* Upload
* Delete

### Can trigger:

* AWS Lambda
* Amazon SNS
* Amazon SQS

---

# 🔁 13. Replication (CRR & SRR)

| Type | Description              |
| ---- | ------------------------ |
| CRR  | Cross-region replication |
| SRR  | Same-region replication  |

### Requirements:

* Versioning must be enabled

---

# 🧹 14. Object Lock & Retention

* Prevents deletion
* Used for compliance (WORM – Write Once Read Many)

---

# 📊 15. Monitoring & Logging

* CloudWatch metrics
* Server access logging
* CloudTrail (API logs)

---

# 💰 16. Pricing Factors

* Storage used
* Requests (GET, PUT)
* Data transfer
* Storage class

---

# ⚠️ 17. Common Interview Scenarios

## ❓ Q1: How do you secure an S3 bucket?

✔ Answer:

* Block public access
* Use IAM roles
* Enable encryption
* Use bucket policies

---

## ❓ Q2: Difference between IAM policy & bucket policy?

✔ Answer:

* IAM → attached to user/role
* Bucket → attached to bucket

---

## ❓ Q3: How to reduce S3 cost?

✔ Answer:

* Lifecycle policies
* Intelligent-tiering
* Delete unused data

---

## ❓ Q4: What happens if you delete an object in versioned bucket?

✔ Answer:

* Delete marker is added (object not actually deleted)

---

## ❓ Q5: How to upload large files?

✔ Answer:

* Multipart upload

---

# 🧠 18. Real-World Architecture Example

👉 Image Upload System:

1. User uploads image → S3
2. S3 triggers Lambda
3. Lambda resizes image
4. Store resized image in another bucket

---

# 🚀 19. Advanced Topics (For 3+ Years Experience)

* S3 Select (query data inside objects)
* Object Lambda
* Access Points
* VPC Endpoints
* Batch Operations

---

# 🧩 20. Quick Revision Cheat Sheet

* Bucket = container
* Object = file
* Key = path/name
* Versioning = backup
* Lifecycle = cost saving
* IAM/Bucket Policy = security
* Glacier = archive
* Multipart = large upload

---

# 🎯 How to Prepare for Interviews

Focus on:

* Real use cases
* Security scenarios
* Cost optimization
* Architecture questions

---

If you want, I can next:
✅ Give you **top 50 S3 interview questions with answers**
✅ Provide **hands-on project (step-by-step)**
✅ Create a **real-world system design using S3**


Got it — let’s go **deep, concept-by-concept**, the way interviewers expect you to *really understand S3*, not just define it.

---

# 🌐 1. Amazon S3 – Deep Understanding

**Amazon S3** from Amazon Web Services is an **object storage system**, not a file system.

### 🔍 What does that mean?

* You **don’t have folders/directories physically**
* Everything is stored as **objects in a flat structure**
* “folders” are just **prefixes in object keys**

👉 Example:

```
bucket: my-data
key: logs/2026/march/app.log
```

S3 sees this as:

```
"logs/2026/march/app.log"
```

NOT nested folders.

---

# 🪣 2. Bucket – Deep Dive

## 🔹 What is a Bucket?

A bucket is:

* A **logical container**
* Region-specific
* Globally unique name

## 🔹 Why globally unique?

Because S3 uses:

```
https://bucket-name.s3.amazonaws.com/object
```

## 🔹 Important Concepts

* **Region matters**

  * Latency
  * Cost
  * Compliance

## 🧠 Interview Insight

> Bucket naming affects DNS routing and global uniqueness ensures no conflicts in AWS infrastructure.

---

# 📦 3. Object – Deep Dive

An object = **data + metadata + key + version**

## 🔹 Components

### 1. Data (Value)

* Actual file (image, video, JSON)

### 2. Key

* Unique identifier inside bucket

### 3. Metadata

* System-defined (size, last modified)
* User-defined (custom tags)

### 4. Version ID

* Only if versioning enabled

---

## 🔹 Object Size Limits

* Min: 0 bytes
* Max: 5 TB
* > 100 MB → use multipart upload

---

# 🔑 4. Key Structure & Prefixes

## 🔹 Key = Full Path

```
user-data/123/profile.png
```

## 🔹 Prefix Concept

* Used for:

  * Logical grouping
  * Performance optimization

## 🔹 Performance Tip

S3 internally distributes load using prefixes.

👉 Bad:

```
logs/1.log
logs/2.log
logs/3.log
```

👉 Better:

```
logs/2026/03/21/1.log
```

---

# 📦 5. Storage Classes – Deep Explanation

Storage classes balance:
👉 Cost vs Access Frequency

---

## 🔹 S3 Standard

* High availability
* Low latency
* Expensive

👉 Use:

* Websites
* Apps

---

## 🔹 S3 Intelligent-Tiering

* Automatically moves objects between tiers

👉 When to use:

* Unknown access patterns

---

## 🔹 S3 Standard-IA

* Cheaper storage
* Higher retrieval cost

👉 Use:

* Backups accessed occasionally

---

## 🔹 S3 One Zone-IA

* Stored in one AZ only

👉 Risk:

* Data loss if AZ fails

---

## 🔹 Glacier

* Archive storage
* Retrieval takes minutes–hours

---

## 🔹 Glacier Deep Archive

* Cheapest
* Retrieval takes hours

---

## 🧠 Interview Insight

> Storage classes are key to cost optimization strategies in cloud architecture.

---

# 🔐 6. Security – Deep Dive (VERY IMPORTANT)

## 🔹 1. IAM Policies

Attached to:

* Users
* Roles

👉 Controls:
WHO can access WHAT

---

## 🔹 2. Bucket Policies

Attached to:

* Bucket

👉 Controls:

* Cross-account access
* Public access

---

## 🔹 3. Block Public Access (Critical)

* Prevents accidental exposure

---

## 🔹 4. Encryption

### SSE-S3

* AWS manages keys

### SSE-KMS

Uses AWS Key Management Service

* Fine-grained control
* Auditing

### SSE-C

* You provide keys

---

## 🧠 Interview Scenario

> “Sensitive data storage?”
> Answer:

* Enable SSE-KMS
* Restrict access via IAM
* Enable logging

---

# 🔄 7. Versioning – Deep Dive

## 🔹 What happens internally?

* Every update creates a **new version**
* Old versions remain

## 🔹 Delete behavior

* Adds **delete marker**
* Doesn’t remove data

---

## 🔹 Why important?

* Protection against:

  * Accidental delete
  * Overwrites

---

# 🗂️ 8. Lifecycle Policies – Deep Dive

Automates object transitions.

## 🔹 Lifecycle Actions

* Transition storage class
* Expire (delete)
* Abort multipart uploads

---

## 🔹 Example Flow

```
Day 0 → S3 Standard
Day 30 → IA
Day 90 → Glacier
Day 365 → Delete
```

---

## 🧠 Interview Insight

> Lifecycle policies are essential for automated cost optimization in large-scale systems.

---

# 🌍 9. Data Consistency

## 🔹 Old (before 2020)

* Eventual consistency

## 🔹 Now

* Strong consistency

👉 Meaning:

* Upload → immediately visible

---

# ⚡ 10. Multipart Upload – Deep Dive

## 🔹 Why needed?

* Large files fail easily
* Slow uploads

## 🔹 How it works?

1. Split file into parts
2. Upload in parallel
3. Combine at end

---

## 🔹 Benefits

* Faster
* Fault-tolerant

---

# 🌐 11. Pre-Signed URLs

## 🔹 What?

Temporary URL to access private object

## 🔹 Why?

* Secure sharing
* No public exposure

---

## 🔹 Example Use Case

* Upload file directly from frontend to S3

---

# 📡 12. Event Notifications – Deep Dive

S3 can trigger:

* AWS Lambda
* Amazon SNS
* Amazon SQS

---

## 🔹 Flow Example

```
Upload → S3 → Lambda → Process image
```

---

# 🔁 13. Replication – Deep Dive

## 🔹 CRR (Cross Region)

* Disaster recovery

## 🔹 SRR (Same Region)

* Compliance

---

## 🔹 Requirements

* Versioning enabled
* IAM role configured

---

# 🧹 14. Object Lock

## 🔹 What?

Prevents deletion

## 🔹 Modes

* Governance
* Compliance

---

## 🔹 Use Case

* Financial records
* Legal data

---

# 📊 15. Monitoring

## 🔹 Tools

* CloudWatch → metrics
* CloudTrail → API logs

---

# 💰 16. Pricing Deep Logic

You pay for:

1. Storage (GB/month)
2. Requests (PUT, GET)
3. Data transfer

---

## 🧠 Interview Insight

> Many systems fail cost optimization due to ignoring request costs, not just storage.

---

# 🧠 17. Real Interview Scenario (Deep)

## ❓ Design: File Upload System

### Solution:

1. Client gets pre-signed URL
2. Uploads to S3 directly
3. S3 triggers Lambda
4. Metadata stored in DB

---

## Why this design?

* Scalable
* Secure
* No backend load

---

# 🚀 18. Advanced Concepts (Deep)

## 🔹 S3 Select

* Query inside objects (like SQL)

## 🔹 Access Points

* Simplifies large bucket access control

## 🔹 VPC Endpoints

* Private access without internet

---

# 🎯 Final Interview Strategy

Focus on:

* WHY (not just WHAT)
* Trade-offs
* Real-world use cases

---

If you want next level:
👉 I can give:

* **Mock interview (with feedback)**
* **Hands-on lab (step-by-step AWS console + CLI)**
* **System design questions using S3**

Just tell me 👍


This is a comprehensive, end-to-end guide to Amazon S3, structured for a deep understanding and to help you ace interview questions. We'll go from foundational concepts to advanced topics.

---

### Phase 1: The Basics - What & Why

#### 1. What is S3?
**Simple Storage Service (S3)** is a object storage service. It's not a file system or a block-level storage (like a hard drive). It's designed to store and retrieve any amount of data from anywhere, over the internet.

**Interview Answer:** "S3 is a highly durable, scalable, and secure object storage service. It's the 'basic building block' of storage on AWS, ideal for storing static files, backups, data lakes, and application assets. Its key differentiators are its 99.999999999% (11 9's) durability and virtually unlimited scalability."

#### 2. Key Terminology
- **Bucket:** A container for objects. Think of it as the root directory. Bucket names are **globally unique** across all AWS accounts.
- **Object:** The actual data (file) and its metadata. Every object has a **key**, which is its unique identifier within a bucket (e.g., `images/logo.png`).
- **Key:** The full path to the object. `folder/sub-folder/file.txt` is all the key.
- **Region:** The physical location where your bucket and its data are stored. Choose a region close to your users for low latency.

**Interview Question:** "How do you ensure a bucket name is unique?"
**Your Answer:** "Bucket names are globally unique across all of AWS, not just my account. So I'd need to choose a name that isn't already taken by anyone else. I can use the AWS CLI or console to check for availability."

---

### Phase 2: Core Concepts - Deep Dive

#### 3. Durability vs. Availability
This is a classic interview distinction.

- **Durability:** The probability of *losing* an object. S3 Standard's durability is **99.999999999% (11 nines)** . This means if you store 10 million objects, you can expect to lose one object once every 10,000 years. This is achieved by automatically replicating data across multiple Availability Zones (AZs) within a region.
- **Availability:** The probability that a *request* to S3 (like a GET or PUT) will succeed. This varies by storage class (e.g., S3 Standard offers 99.99% availability).

**Interview Answer:** "Durability is about data loss prevention; availability is about uptime. S3's 11 nines of durability is achieved through automatic, redundant storage across multiple Availability Zones. Availability is a service-level metric that varies depending on the storage class I choose, balancing cost against accessibility needs."

#### 4. Storage Classes (Tiers)
Choosing the right class is critical for cost optimization.

| Storage Class | Use Case | Key Feature | Availability |
| :--- | :--- | :--- | :--- |
| **S3 Standard** | Frequently accessed, critical data. Low latency, high throughput. | High durability & high availability. | 99.99% |
| **S3 Intelligent-Tiering** | Unknown or changing access patterns. | Automatically moves data between frequent and infrequent access tiers. Adds a monitoring fee but no retrieval fees. | 99.9% |
| **S3 Standard-IA (Infrequent Access)** | Long-lived, less frequently accessed data (e.g., backups, disaster recovery). | Lower storage cost, but has a **retrieval fee** per GB. | 99.9% |
| **S3 One Zone-IA** | Infrequent access data where losing an AZ is acceptable (e.g., re-creatable data). | Same cost as IA, but **data is in only one AZ**. Lower durability. | 99.5% |
| **S3 Glacier Instant Retrieval** | Long-term archives requiring millisecond retrieval. | Archive with instant access. | 99.9% |
| **S3 Glacier Flexible Retrieval** | Long-term archives where retrieval time is flexible (minutes to hours). | Very low storage cost; retrieval times: expedited (1-5 min), standard (3-5 hrs), bulk (5-12 hrs). | 99.99% (after restore) |
| **S3 Glacier Deep Archive** | Long-term compliance, digital preservation. | Lowest storage cost; retrieval time: standard (12 hrs), bulk (48 hrs). | 99.99% (after restore) |

**Interview Question:** "How would you decide between Standard-IA and Glacier?"
**Your Answer:** "I'd look at the access pattern. If I need to access the data frequently, Standard is best. If it's long-lived but accessed, say, once a quarter, Standard-IA is a good fit despite retrieval fees. If the data is for compliance and I only need it once a year or less, I'd go with Glacier Flexible or Deep Archive for maximum cost savings."

#### 5. Versioning
- **What it is:** A mechanism to keep multiple versions of an object in the same bucket.
- **Why use it:** Protects against accidental deletions (a delete becomes a "delete marker") and overwrites. Once enabled, it **cannot be disabled**, only suspended.
- **Cost implication:** You pay for each version stored. So, managing old versions with lifecycle policies is crucial.

#### 6. Lifecycle Policies
Automate the transition of objects between storage classes or expire (delete) them.

- **Transitions:** Move objects to colder storage. E.g., "Move from Standard to Standard-IA after 30 days, then to Glacier after 90 days."
- **Expirations:** Delete objects. E.g., "Delete objects in the 'logs/' folder after 365 days."
- **For Versioning:** "Permanently delete older versions after 30 days."

**Interview Question:** "How do you prevent your S3 bill from blowing up due to storage costs?"
**Your Answer:** "By implementing a combination of storage class selection and, more importantly, robust lifecycle policies. For example, I'd use Intelligent-Tiering for unpredictable workloads, and for logs, I'd have a policy to transition them to Glacier after a week and expire (delete) them after a year. If versioning is enabled, I'd also have a separate policy to clean up old, non-current versions."

---

### Phase 3: Security & Access Control

#### 7. Security Layers (The 3 Pillars)
Security in S3 is a shared responsibility. You control access with three main mechanisms:

1.  **IAM Policies:** Define what users, groups, or roles in your AWS account can do. E.g., "User 'dev-user' can list and read objects from `my-bucket`."
2.  **Bucket Policies:** JSON-based policies attached *directly to the bucket*. Used for cross-account access, making buckets public, or enforcing conditions (like MFA or HTTPS).
3.  **ACLs (Access Control Lists):** An older, legacy mechanism. Best practice is to use **ACLs disabled** and rely on IAM/Bucket Policies.

**Interview Scenario:** "How would you grant read-only access to an S3 bucket to a user from another AWS account?"
**Your Answer:** "I would use a **bucket policy**. I'd write a policy that grants the `s3:GetObject` permission to the root user or a specific role from the other AWS account. I'd also ensure the user in that account has an IAM policy allowing them to assume that permission. I would not use ACLs for this."

#### 8. Encryption (Data at Rest & In Transit)
- **In Transit:** Enforce **HTTPS/TLS** using bucket policies (e.g., `"aws:SecureTransport": "false"` to deny non-HTTPS requests).
- **At Rest:** Three ways to encrypt objects:
    - **SSE-S3 (Server-Side Encryption with S3-Managed Keys):** AWS handles the keys. Simple, default option.
    - **SSE-KMS (Server-Side Encryption with KMS-Managed Keys):** Use AWS Key Management Service. Provides separate permissions control, audit trail, and automatic key rotation. **Adds KMS costs.**
    - **SSE-C (Server-Side Encryption with Customer-Provided Keys):** You manage the keys; AWS manages the encryption process.

**Interview Question:** "What's the difference between SSE-S3 and SSE-KMS?"
**Your Answer:** "SSE-S3 is the default, where S3 manages the master keys. SSE-KMS gives me more control. With KMS, I can have separate permissions for key usage, get a CloudTrail audit of who used which key, and set up automatic key rotation. However, it does come with additional costs for KMS API calls."

#### 9. Pre-Signed URLs
Generate a time-limited URL to grant temporary access to a private object without changing the object's ACL or bucket policy.

- **Use Cases:**
    - Allow a user to download a private file (e.g., a purchase receipt).
    - Allow a user to upload a file directly to a specific folder without having AWS credentials.
- **Mechanism:** You, the AWS user with permissions, generate the URL. The permissions are embedded in the URL signature.

---

### Phase 4: Performance & Optimization

#### 10. Performance Optimization
- **High Request Rates:** S3 scales automatically. For high **prefix-level** throughput, you can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second *per prefix*.
    - **Tip:** To maximize performance, spread your keys across multiple prefixes. Don't use sequential IDs (like `timestamp-file1`) as keys; use random prefixes (e.g., `hash-timestamp-file1`).
- **Multipart Upload:** For objects > 100 MB, and mandatory for > 5 GB. It uploads parts in parallel, increasing throughput and allowing for easy retries of failed parts.
- **S3 Transfer Acceleration:** Uses AWS edge locations to speed up uploads over long distances. Good for cross-continental uploads but costs extra.

---

### Phase 5: Advanced Features & Patterns

#### 11. S3 Event Notifications
Trigger workflows based on S3 events (e.g., `s3:ObjectCreated:*`, `s3:ObjectRemoved:*`). Events can be sent to:
- **AWS Lambda:** For serverless processing (e.g., image resizing, video transcoding).
- **Amazon SNS:** For sending notifications.
- **Amazon SQS:** For decoupled processing in a queue.

#### 12. Cross-Region Replication (CRR) & Same-Region Replication (SRR)
- **CRR:** Automatically replicates objects to a bucket in a different region.
    - **Use Cases:** Compliance, lower latency for global users, disaster recovery.
- **SRR:** Replicates within the same region.
    - **Use Cases:** Aggregate logs from multiple accounts into a central bucket, maintain copies in a different account for security.

**Important:** Replication requires versioning to be enabled on both source and destination buckets.

#### 13. Static Website Hosting
S3 can host static websites (HTML, CSS, JS, client-side code). You enable the feature on a bucket, configure it as public, and set the index and error documents.

**Note:** For HTTPS and more advanced features (like custom headers, routing rules), you'd place **Amazon CloudFront** (AWS's CDN) in front of the S3 bucket.

---

### Phase 6: Data Management & Operations

#### 14. S3 Batch Operations
A way to perform bulk actions (e.g., copy, tag, restore from Glacier, invoke a Lambda function) on a large list of objects (millions or billions) with a single request. You provide a manifest (list of objects) and S3 manages the job, providing progress reports and completion notifications.

#### 15. S3 Access Points & Access Point Policies
A feature to simplify managing access at scale. Instead of one bucket policy with hundreds of permissions, you create **Access Points**, each with its own policy, network controls, and permissions.

- **Example:** Create `access-point-for-finance-team` with a policy allowing only GET requests from the finance team's VPC.

#### 16. S3 Object Lambda
Add custom logic to S3 GET requests. You add a Lambda function that modifies the data *on the fly* before it's returned to the requester.

- **Use Cases:** Redacting personally identifiable information (PII) from documents, converting file formats dynamically, injecting watermarks.

---

### Final Interview Simulation

**Interviewer:** "You need to design a secure, cost-optimized solution to store user profile pictures. Users upload pictures once, they are viewed frequently for the first 30 days, and then rarely after that. Compliance requires that all data be retained for 7 years. How would you design this in S3?"

**Your Comprehensive Answer:**
"I would design it with the following layers:

1.  **Buckets & Permissions:** I'd use two buckets: a 'private-uploads' bucket and a 'public-serve' bucket. The upload bucket would have a bucket policy to deny public access and enforce HTTPS. I'd use a **pre-signed URL** approach for uploads. Upon upload completion, an **S3 Event Notification** would trigger a **Lambda function**.
2.  **Processing:** The Lambda function would download the image, resize it for performance, and re-upload it to the 'public-serve' bucket with public-read permissions. It would also encrypt it using **SSE-KMS** for key management and audit trails.
3.  **Storage Classes:** The 'public-serve' bucket would use **Intelligent-Tiering** because access starts high and drops off. The original high-res version in the 'private-uploads' bucket, which is rarely accessed, would be moved to **S3 Glacier Flexible Retrieval** after 30 days via a **lifecycle transition**.
4.  **Cost Optimization:** I'd use a **lifecycle policy** to expire (delete) old versions of objects if versioning is enabled, to avoid paying for old, non-current versions. I'd also set up a separate lifecycle rule to automatically delete objects after 7 years to comply with retention but not over-pay for storage.
5.  **Performance:** For global distribution, I'd put **Amazon CloudFront** in front of the public-serve bucket. This provides edge caching for the frequently accessed images, drastically reducing S3 GET costs and improving latency."

This structure shows you don't just know S3 concepts, but you can architect a solution using multiple S3 features together. Good luck with your learning and interviews
