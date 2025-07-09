
# 📦 Project 2: Azure Storage Account + RBAC

## 🧾 Overview
This lab focuses on configuring an Azure Storage Account with secure access and lifecycle management. The goal is to gain hands-on experience with storage redundancy, RBAC, SAS tokens, and data tiering.

---

## ✅ Objectives
- Create a storage account with proper redundancy
- Upload blob files and create a file share
- Generate a SAS token with limited permissions
- Assign RBAC roles to control access
- Enable soft delete and lifecycle policies for archiving

---

## 🛠️ Steps

### 1. Create a Resource Group
- **Name:** `RG-AZ104-StorageLab`

![Resource Group](https://github.com/abarnes285/AZ-104-LABS/blob/f569e59c80e6e258d1ec49a666027f6304379c73/Azure%20Storage%20account%20/Images/image%201.png)

---

### 2. Create a Storage Account
- **Name:** `az104storageproj`
- **Redundancy:** Locally Redundant Storage (LRS)
- **Region:** Same as Resource Group
- **Enabled SFTP**

![Storage Account](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%202.png)

---

### 3. Create Blob Container and Upload File
- Created container: `project2container`
- Uploaded a PNG file
- Changed access tier to **Cool**

![Container](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%203.png)
![File Upload](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%204.png)
![Tier Changed](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%205.png)

---

### 4. Generate SAS Token
- Created **SAS token** with Read/Write permissions
- Initial token failed to work
- Resolved by generating a token at the **container level**

![SAS Token Config](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%206.png)
![SAS Token Error](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%208.png)
![Working SAS Token](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%209.png)

---

### 5. Enable Soft Delete & Lifecycle Management
- Enabled **soft deletion** for blobs (7-day retention)
- Configured lifecycle rule to archive older blobs

![Soft Delete Enabled](https://github.com/abarnes285/AZ-104-LABS/blob/511c7b79a05f375c3cd21edaf2eb15d5e810c1fe/Azure%20Storage%20account%20/Images/image%2010.png)

---

## 🔐 Securing Azure Storage
- Restricted access through **RBAC role assignments**
- Used SAS token with limited scope instead of account-level keys
- Enabled soft delete to protect against accidental deletions

---

## ⚠️ Challenges Faced
- SAS token did not initially grant access when generated at the storage account level.
  - ✅ Fixed by generating the token directly from the container resource.

---

## 💡 Skills Practiced
- Azure Storage Configuration
- Blob Access Management (SAS + RBAC)
- Soft Delete and Lifecycle Policies
- Storage Tiering (Hot → Cool)

---

## 🔗 Tags
`#Azure #AZ104 #BlobStorage #RBAC #SASToken #StorageSecurity #CloudProjects #LearningInPublic`
