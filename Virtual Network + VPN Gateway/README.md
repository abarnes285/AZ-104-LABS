# 🌐 Project 3: Virtual Network + VPN Gateway Lab

This project demonstrates how to build a hub-spoke network architecture in Azure, configure a VPN Gateway for Point-to-Site (P2S) connectivity, and establish secure communication between on-premises clients and Azure resources.

---

## 🏗️ Step 1: Resource Group & VNets

- Created a resource group: **RG-HubSpoke-Lab**

  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image.png)

- Created a Hub VNet: **Vnet-Hub** and assigned it to the resource group

  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%201.png)

- Added a subnet **HubSubnet** to the VNet

  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%202.png)

- Created **Vnet-Spoke1** and added a subnet

  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%203.png)

- Created **Vnet-Spoke2** and added a subnet

  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%204.png)

---

## 🔗 Step 2: VNet Peering

- Enabled peering from Hub to Spoke1  
  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%205.png)

- Enabled peering from Hub to Spoke2  
  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%206.png)

---

## 🚪 Step 3: VPN Gateway Setup

- Created a **GatewaySubnet**  
  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%207.png)

- Created a **Public IP** for the VPN Gateway  
  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%208.png)

- **Deployed the VPN Gateway**:
  - Assigned it to the resource group
  - Linked to the Hub VNet and VPN subnet
  - Assigned static public IP  
  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/8ba6bb47e0001ca3af506dab659d3bb5412aa068/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%209.png)

---

## 🔐 Step 4: Create Root Certificate for P2S

Generated a self-signed root certificate using PowerShell:

```powershell
$rootCert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=MyP2SRootCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-KeyUsageProperty Sign -KeyUsage CertSign

| Parameter                                   | Description                                                          |
| ------------------------------------------- | -------------------------------------------------------------------- |
| `$rootCert =`                               | Stores the certificate object in a variable for later use            |
| `New-SelfSignedCertificate`                 | Cmdlet to generate a new self-signed certificate                     |
| `-Type Custom`                              | Creates a custom certificate with full configuration options         |
| `-KeySpec Signature`                        | Indicates the certificate is used for digital signatures             |
| `-Subject "CN=MyP2SRootCert"`               | Sets the Common Name (CN) for the certificate                        |
| `-KeyExportPolicy Exportable`               | Allows the certificate’s private key to be exported                  |
| `-HashAlgorithm sha256`                     | Uses the SHA-256 hashing algorithm for encryption                    |
| `-KeyLength 2048`                           | Specifies the key length (2048-bit RSA), Azure's recommended minimum |
| `-CertStoreLocation "Cert:\CurrentUser\My"` | Location in the certificate store where it will be saved             |
| `-KeyUsageProperty Sign -KeyUsage CertSign` | Marks the certificate for signing other certificates (acts as a CA)  |
```

## 🧾 Step 5: Export Certificate

After creating the root certificate, I exported it using the following PowerShell command:

```powershell
Export-Certificate -Cert $rootCert -FilePath "C:\MyP2SRootCert.cer"
| Parameter            | Description                                                   |
| -------------------- | ------------------------------------------------------------- |
| `Export-Certificate` | PowerShell cmdlet used to export a certificate to a file      |
| `-Cert $rootCert`    | Specifies the certificate object to export                    |
| `-FilePath "C:\..."` | Defines the full path where the exported `.cer` file is saved |
```
 Issue: When opening the file in Notepad, I saw binary data (unreadable characters), which meant the certificate was exported in binary format instead of Base64.
  ![image](https://github.com/abarnes285/AZ-104-LABS/blob/05743f682dfd445de9176883ee64a184c1b86cc0/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%2011.png)
   ![image](https://github.com/abarnes285/AZ-104-LABS/blob/05743f682dfd445de9176883ee64a184c1b86cc0/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%2012.png)
## 🔄 Step 6: Export as Base64
🛠️ Solution Attempted
To resolve this, I updated the command to specify the export type explicitly:
```Powershell
Export-Certificate -Cert $rootCert -FilePath "C:\Users\andrew.barnes\Desktop\MyP2SRootCert.cer" -Type CERT
```
✅ This command was intended to export the certificate as a Base64-encoded X.509 file.
However, the resulting file still appeared in binary format when opened with a text editor. This led to the next step: manual export via MMC, which is covered in Step 7. 
## 🔄 Step 7: Manually Export Certificate to Base64

After multiple failed attempts to export the certificate as Base64 using PowerShell, I switched to the **MMC (Microsoft Management Console)** to export the certificate in the correct format manually.

### 🛠 Steps to Export as Base64-Encoded X.509 (.CER)

1. Press `Win + R`, type `mmc`, and press Enter
2. Go to **File > Add/Remove Snap-in**
3. Select **Certificates** and click **Add**
4. Choose **My user account** and click **Finish**, then **OK**
5. In the left pane, navigate to:
 ![image](https://github.com/abarnes285/AZ-104-LABS/blob/be91dd1424d9df3d1c3d5ecabd414e2ff30fb6ee/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%2015.png)
Certificates (Current User) > Personal > Certificates
![image](https://github.com/abarnes285/AZ-104-LABS/blob/be91dd1424d9df3d1c3d5ecabd414e2ff30fb6ee/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%2016.png)
6. Locate the certificate (`MyP2SRootCert`) you created
7. Right-click the cert → **All Tasks** → **Export**
8. In the Certificate Export Wizard:
- Select **No, do not export the private key**
- Choose **Base-64 encoded X.509 (.CER)**
- Choose a file path (e.g., Desktop) and export the file
![image](https://github.com/abarnes285/AZ-104-LABS/blob/be91dd1424d9df3d1c3d5ecabd414e2ff30fb6ee/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%2017.png)

### ✅ Result

- The exported certificate can now be opened in a text editor (e.g., Notepad)
- It will be human-readable and look like this:
![image](https://github.com/abarnes285/AZ-104-LABS/blob/be91dd1424d9df3d1c3d5ecabd414e2ff30fb6ee/Virtual%20Network%20%2B%20VPN%20Gateway/Images/image%2019.png)

