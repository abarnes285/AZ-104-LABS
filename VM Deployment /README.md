
# Azure Lab: VM Deployment and Configuration

## 🧾 Overview
This lab walks through deploying two Azure VMs in an availability set with security, monitoring, and cost-saving configurations.

## ✅ Objectives
- Deploy 2 VMs into an availability set
- Assign public and private IP addresses
- Configure NSGs to restrict RDP and SSH access
- Add managed disks
- Enable auto-shutdown and monitoring
-  Connect via RDP and configure system settings
- Set tagging and enable alerting via Log Analytics

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
- Did not modify outbound rules (default allowed)
- Associated NSG with the appropriate subnet

![NSG Rules](https://github.com/abarnes285/AZ-104-LABS/blob/c9d574c876856c6d358163ba6ac3bfe912405a3e/VM%20Deployment%20/Images/image%202.png)

![NSG Subnet](https://github.com/abarnes285/AZ-104-LABS/blob/c9d574c876856c6d358163ba6ac3bfe912405a3e/VM%20Deployment%20/Images/image%203.png)

---

### 4. Deploy the VMs
- Selected the subnet associated with the VNet
- Assigned public and private IPs
- Attached NSG during setup
- Enabled auto-shutdown (7:00 PM)
- Enabled Site Recovery vault
- Enabled alerting for CPU usage > 80%
- Connected via RDP after deployment

![VM Deployed](https://github.com/abarnes285/AZ-104-LABS/blob/6227be2d99b27af133e2494d3e2a92c7545e5726/VM%20Deployment%20/Images/image%204.png)

![VM Deployed](https://github.com/abarnes285/AZ-104-LABS/blob/6227be2d99b27af133e2494d3e2a92c7545e5726/VM%20Deployment%20/Images/image%205.png)

![VM Deployed](https://github.com/abarnes285/AZ-104-LABS/blob/6227be2d99b27af133e2494d3e2a92c7545e5726/VM%20Deployment%20/Images/image%205.png)

![Monitoring Setup](https://github.com/abarnes285/AZ-104-LABS/blob/6227be2d99b27af133e2494d3e2a92c7545e5726/VM%20Deployment%20/Images/image%206.png)

---

### 5. Post-Deployment Configuration
- Installed Windows updates
- Changed the time zone
- Tagged each VM with:
  - `Environment`
  - `Purpose`
  - `Owner`
 


![VM Updates](https://github.com/abarnes285/AZ-104-LABS/blob/6227be2d99b27af133e2494d3e2a92c7545e5726/VM%20Deployment%20/Images/image%209.png)

![VM Time](https://github.com/abarnes285/AZ-104-LABS/blob/6227be2d99b27af133e2494d3e2a92c7545e5726/VM%20Deployment%20/Images/image%2010.png)

![VM Tags](https://github.com/abarnes285/AZ-104-LABS/blob/6227be2d99b27af133e2494d3e2a92c7545e5726/VM%20Deployment%20/Images/image%2011.png)

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


