# AWS IAM, EBS, S3, VPC, CIDR & NAT – Clean Notes

---

## 🖼️ AWS Image Building Pipeline
→ Used to create reusable images (AMIs)  
→ Snapshot → Image → Launch instances

---

## 🔐 Identity Access Management (IAM)

→ AWS is compliant, but **security of our resources is our responsibility**  
→ IAM tells us:
```

Who can do WHAT
on WHICH resource

```

---

### IAM Core Concepts

```

Identity  →  Action  →  Resource

```

- **Identity**
  → User / Group / Role

- **Action**
  → Decided by permissions
  → Read, Write, Delete, etc.

- **Resource**
  → AWS services
  → Foundation services (4+)
  → Bucket services (50+)

→ IAM also controls **access from outside the AWS world**

---

## 📜 IAM Policies

→ AWS has **4000+ permissions**  
→ From these permissions, we create **policies**

→ **Policy**
- A collection of permissions
- Written in JSON
- Defines what actions are allowed or denied

→ AWS provides **200+ predefined (managed) policies**

→ Policies are:
- Picked up
- Attached to the **right identity** (user / group / role)

---

## 🏗️ IAM Hierarchy

```

ORG (All Policies)
|
|-- Dev        (Some policies)
|     |
|     |-- S1 (Users)
|           |-- B1
|           |-- B2
|           |-- B3
|
|-- Testing   (Some policies)
|     |
|     |-- S2 (Users)
|           |-- B1
|           |-- B2
|           |-- B3
|
|-- Support   (Some policies)
|
|-- S3 (Users)
|-- B1
|-- B2

````

→ Policies flow **top-down**

---

## 📏 IAM Rules

### Rule of Least Privilege
→ Always give users **least required permissions**

---

### Parent–Child Relationship

→ Child can inherit what parent has  
→ Child may need **extra IAM permissions**  
→ If parent does not have IAM permission,
  child **will not get it automatically**

---

## 💾 Resize EBS Volume

### Steps

1. Identify the volume
2. Create a **snapshot**
3. Create a **new volume** from snapshot
4. Resize the new volume
5. Detach old volume
6. Attach resized volume

---

### Points to Remember

- Zone of volume creation must be **same as VM**
- Storage type / root device:
  - Linux → `/xvda`
  - Windows → `/sda`

---

### Validation Commands

```bash
df -h           # Check disk size
ping google.com # Check network connectivity (timeout may change)
````

---

## 🖼️ Create Image (AMI)

→ Create snapshot for the volume
→ Select snapshot
→ Create image via **Actions**

---

## 🧰 AWS CLI Commands

```bash
aws --version             # Verify AWS CLI
aws configure             # Configure user
aws s3 ls                 # List S3 buckets
```

### Copy Files to S3

```bash
aws s3 cp <source-file> s3://bucket-name
```

### Copy Between Buckets

```bash
aws s3 cp s3://bucket1/file s3://bucket2/file
```

### Create Bucket

```bash
aws s3 mb s3://bucket-name
```

---

## 🌐 VPC (Virtual Private Cloud)

→ Framework for **networking & security settings**

Key points:

* Contains **subnets**
* Services are launched inside subnets
* **Max 6 subnets** allowed (as per notes)

---

### EC2 Networking Flow

```
VPC
 |
 |-- Subnet
       |
       |-- EC2
```

→ EC2 security is applied:

1. Network level
2. Subnet level
3. EC2 level

---

## 🧱 CIDR Block

→ CIDR defines **IP address range**

Example:

```text
10.0.0.0/26
```

→ Formula:

```
2^(32 - x) = Total IPs
```

For `/26`:

```
2^(32 - 26) = 64 IPs
```

→ 64 resources allowed in the VPC

---

## 🔹 Subnet CIDR Calculation

→ Divide 64 IPs into 2 subnets

### Subnet 1

```text
10.0.0.0/27
IP range: 0–31
```

### Subnet 2

```text
10.0.0.32/27
IP range: 32–63
```

---

## 🔐 Network Components

* **Route Table**
* **NACL (Network Access Control List)**
* **Security Group**

---

### Network Security Levels

* **EC2 level**
  → Security Group

* **Subnet level**
  → NACL

* **VPC level**
  → Gateways + Route Tables

---

## 🌍 IP Address

→ IP address is the **first requirement** for networking

---

## 🔁 Launch VPC with Multiple Subnets

→ Each subnet has:

* Its own CIDR
* Own routing rules

---

## 🌐 NAT (Network Address Translation)

→ Used when:

* Indirect internet communication is required
* Additional security layer is needed

→ NAT enables **private resources** to access the internet
→ Prevents direct inbound internet access

---

## ✅ Summary

* IAM controls *who can do what on which resource*
* Policies are JSON-based permission sets
* Least privilege is a core IAM rule
* EBS resizing uses snapshot → new volume
* S3 is managed via AWS CLI
* VPC defines networking boundaries
* CIDR controls IP allocation
* NAT provides secure outbound internet access
