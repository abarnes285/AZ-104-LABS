
# Azure Lab: VM Deployment and Configuration

## 🧾 Overview
This lab walks through deploying two Azure VMs in an availability set with security, monitoring, and cost-saving configurations.

## ✅ Objectives
- Deploy 2 VMs into an availability set
- Assign public and private IP addresses
- Configure NSGs to restrict RDP and SSH access
- Add managed disks
- Enable auto-shutdown and monitoring

---

## 🛠️ Steps

### 1. Create a Resource Group
`RG-ProdVM-EastUS`

![Resource Group Setup](https://github.com/abarnes285/AZ-104-LABS/blob/d79ff299d50432407578ada73648bf672bc7df74/VM%20Deployment%20/Images/image%2013.png)

---

### 2. Create a Virtual Network (VNet)
`VNET-PROD`

![VNet Setup](https://github.com/abarnes285/AZ-104-LABS/blob/c9d574c876856c6d358163ba6ac3bfe912405a3e/VM%20Deployment%20/Images/image%201.png)

---

### 3. Create and Configure Network Security Group (NSG)
- Allow inbound RDP (TCP 3389) and SSH (TCP 22)
- Associate with the appropriate subnet

![NSG Rules](https://github.com/abarnes285/AZ-104-LABS/blob/c9d574c876856c6d358163ba6ac3bfe912405a3e/VM%20Deployment%20/Images/image%202.png)

![NSG Subnet](https://github.com/abarnes285/AZ-104-LABS/blob/c9d574c876856c6d358163ba6ac3bfe912405a3e/VM%20Deployment%20/Images/image%203.png)

---

### 4. Deploy the VMs
- Assign to the availability set and subnet
- Attach NSG and managed disks
- Enable auto-shutdown at 7 PM
- Set up tags and connect via RDP

![VM Deployed](images/vm-deployed.png)

---

### 5. Monitoring and Alerts
- Enable Log Analytics Workspace
- Set alert for CPU > 80%
- Confirm email alert functionality

![Monitoring Setup](images/monitoring-setup.png)

---

## ⚠️ Challenges & Lessons Learned
- Encountered region restriction for Site Recovery Vault in West US — resolved by switching to East US 2
- NSG rule logic required extra attention, especially source vs. destination port handling

---

## 🧠 Key Takeaways
This lab provided a full end-to-end deployment experience while sharpening my Azure VM, networking, and monitoring skills.

---

## 🔗 Tags
`#Azure #Cloud #AZ104 #VMDeployment #Monitoring #NSG #LearningInPublic`


