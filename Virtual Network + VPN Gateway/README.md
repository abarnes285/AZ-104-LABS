# 🌐 Project 3: Virtual Network + VPN Gateway Lab

This project demonstrates how to build a hub-spoke network architecture in Azure, configure a VPN Gateway for Point-to-Site (P2S) connectivity, and establish secure communication between on-premises clients and Azure resources.

---

## 🏗️ Step 1: Resource Group & VNets

- Created a resource group: **RG-HubSpoke-Lab**

  ![image](image.png)

- Created a Hub VNet: **Vnet-Hub** and assigned it to the resource group

  ![image](image%201.png)

- Added a subnet **HubSubnet** to the VNet

  ![image](image%202.png)

- Created **Vnet-Spoke1** and added a subnet

  ![image](image%203.png)

- Created **Vnet-Spoke2** and added a subnet

  ![image](image%204.png)

---

## 🔗 Step 2: VNet Peering

- Enabled peering from Hub to Spoke1  
  ![image](image%205.png)

- Enabled peering from Hub to Spoke2  
  ![image](image%206.png)

---

## 🚪 Step 3: VPN Gateway Setup

- Created a **GatewaySubnet**  
  ![image](image%207.png)

- Created a **Public IP** for the VPN Gateway  
  ![image](image%208.png)

- **Deployed the VPN Gateway**:
  - Assigned it to the resource group
  - Linked to the Hub VNet and VPN subnet
  - Assigned static public IP  
  ![image](image%209.png)

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

