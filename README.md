# 🌐 Azure Networking and Storage

**Topics Covered:** Virtual Networks (VNets), Network Security Groups (NSGs), Storage Accounts, Encryption, Private Endpoints, Shared Access Signatures (SAS), ARM Templates

---

<p align="center">
  <img src="azurenetworkingandstorage.png" alt="Azure Networking and Storage">
</p>

---

## 📖 Summary

This project focuses on building a secure Azure networking and storage environment. It demonstrates how to create Virtual Networks and subnets, secure traffic using Network Security Groups (NSGs), deploy encrypted Storage Accounts with Private Endpoints, and automate deployments using Azure Resource Manager (ARM) templates.

---

## 🏢 Scenario

A company wants to deploy a secure storage solution, isolate network resources using Virtual Networks and Network Security Groups, enforce encryption for data protection, and automate infrastructure deployment using ARM templates.

---

## 🛠️ Steps

### 1️⃣ 🌐 Create a Virtual Network (VNet)

- Navigate to **Azure Portal** → **Virtual Networks** → **Create**.
- Configure a new Virtual Network.
- Create two subnets:
  - **Database**
    - Address Range: `10.0.0.0/27`
    - Enable **Private Subnet**
    - Enable **Service Endpoints** for **Microsoft.Storage**
  - **Web**
    - Address Range: `10.0.1.0/27`
- Review and create the VNet.
- Verify that Azure automatically enables communication between subnets within the same VNet.

---

### 2️⃣ 🔒 Deploy a Network Security Group (NSG)

- Navigate to **Network Security Groups** → **Create**.
- Create a new NSG.
- Associate the NSG with the **Web** subnet:
  - Resource → **Subnets** → **Associate**
- Configure inbound security rules:
  - Allow HTTPS (Port 443) from the Internet
  - Deny all other inbound Internet traffic
- To add the HTTPS rule:
  - **Inbound Security Rules** → **Add**
  - Service: **HTTPS**
  - Destination Port: **443**
- To deny other inbound traffic:
  - Add a rule with Destination Port: `*`
- Review default NSG rules:
  - AllowVnetInBound
  - AllowAzureLoadBalancerInBound
  - DenyAllInBound
- Note that custom rules with higher priority can override default behavior.

---

### 3️⃣ 💾 Create and Configure a Storage Account

- Navigate to **Storage Accounts** → **Create**.
- Configure the following settings:
  - Replication:
    - Locally Redundant Storage (LRS), or
    - Geo-Redundant Storage (GRS)
  - Encryption:
    - Microsoft-managed keys
- Configure secure network access:
  - Navigate to **Advanced**
  - Select:
    - **Permitted Scope** → Storage accounts with private endpoints
  - Disable public access
  - Create a **Private Endpoint**
  - Associate the endpoint with the **Database** subnet
- Review and create the Storage Account.

---

### 4️⃣ ⚙️ Deploy Resources Using ARM Templates

- Navigate to the deployed Virtual Network.
- Select **Automation** → **Export Template**.
- Download the template files.
- Repeat for the Storage Account.
- Navigate to **Template Specs**.
- Select **Import Template**.
- Upload the exported `template.json` file.
- Create the Template Spec.
- Select the three-dot menu (**...**) beside the template.
- Choose **Deploy**.
- Verify that the resources deploy successfully from the template.

---

### 5️⃣ 🔑 Test Access and Encryption

- Navigate to the Storage Account.
- Select **Security + Networking** → **Shared Access Signature (SAS)**.
- Configure:
  - Allowed Resource Types: **All**
- Generate the SAS token.

#### Test Using Azure Storage Explorer

- Install Azure Storage Explorer.
- Select **Connect to Azure Resources**.
- Choose **Use a Shared Access Signature (SAS) URI**.
- Paste the generated connection string or SAS URL.
- Create a Blob Container.
- Upload and download files to verify access.

#### Test Using AzCopy

- Install AzCopy.
- Upload a file using the following command:

```bash
azcopy copy "file-to-upload.txt" "https://yourstorageaccount.blob.core.windows.net/container-name/file-to-upload.txt?[SAS]"
```

- Replace `[SAS]` with the generated SAS token.
- Verify that the file uploads successfully.
- Confirm that encrypted storage and secure access are functioning correctly.

---

## 🎯 Learning Outcomes

By completing this project, you will be able to:

- Create and configure Azure Virtual Networks
- Design subnet architectures for workload isolation
- Secure network traffic using Network Security Groups
- Deploy and configure Azure Storage Accounts
- Implement Private Endpoints for secure storage access
- Enable encryption for data at rest
- Generate and use Shared Access Signatures (SAS)
- Automate deployments using ARM Templates
- Validate secure storage connectivity and access controls

---

## ✅ Services Used

- Azure Virtual Network (VNet)
- Azure Subnets
- Network Security Groups (NSGs)
- Azure Storage Account
- Azure Private Endpoint
- Azure Resource Manager (ARM) Templates
- Azure Storage Explorer
- AzCopy

---

## 📚 Key Concepts

| Feature | Purpose |
|----------|----------|
| Virtual Network (VNet) | Provides network isolation and communication between Azure resources |
| Subnets | Segment workloads within a VNet |
| Network Security Group (NSG) | Controls inbound and outbound network traffic |
| Storage Account | Stores Azure data objects securely |
| Private Endpoint | Enables private access to Azure services |
| Encryption | Protects data at rest using managed keys |
| Shared Access Signature (SAS) | Provides delegated, time-limited access to storage resources |
| ARM Templates | Automate and standardize infrastructure deployments |

This project provides hands-on experience with Azure networking, secure storage design, access control, encryption, and infrastructure-as-code deployment practices.