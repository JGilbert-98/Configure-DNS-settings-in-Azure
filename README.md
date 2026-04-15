# Configure DNS settings in Azure

M01 - Configure DNS Settings in Azure
# Lab Overview

This lab demonstrates how to configure Azure Private DNS for internal name resolution across virtual machines.
---
# Objectives
- Create a Private DNS Zone
- Link a Virtual Network with auto-registration
- Deploy Virtual Machines
- Verify DNS resolution using nslookup
---
# Architecture

<img width="879" height="304" alt="image" src="https://github.com/user-attachments/assets/fd2e3a71-cc35-4aa0-8c84-dbfe30624d98" />



# Implementation Steps
1. Create Private DNS Zone
Name: contoso.com
Resource Group: ContosoResourceGroup
---
2. Link Virtual Network
VNet: CoreServicesVnet
Auto-registration: Enabled
---
3. Deploy Virtual Machines
```
$RGName = "ContosoResourceGroup"

New-AzResourceGroupDeployment `
  -ResourceGroupName $RGName `
  -TemplateFile azuredeploy.json `
  -TemplateParameterFile azuredeploy.parameters.json
```
---
4. Verify DNS Resolution
```
nslookup TestVM2.contoso.com
```
Internal hostname successfully resolved
<img width="447" height="197" alt="image" src="https://github.com/user-attachments/assets/9bb9a263-b3ab-4021-8778-8194edd961ec" />

---
# Screenshots
DNS Zone

<img width="1363" height="473" alt="image" src="https://github.com/user-attachments/assets/5bd7e3a1-f892-4fd8-aaf0-b575dadd5539" />



VNet Link

<img width="1570" height="445" alt="image" src="https://github.com/user-attachments/assets/c012621f-af61-4b50-9e8d-791867cade61" />



VM Records

<img width="1757" height="383" alt="image" src="https://github.com/user-attachments/assets/28306428-7e47-4624-91f4-af07839e4d9c" />



DNS Test

<img width="1369" height="578" alt="image" src="https://github.com/user-attachments/assets/5cf83a4c-7bea-4304-aaff-92bd048b1b9c" />


---
# Key Learnings
- Private DNS Zones enable secure internal name resolution
- Auto-registration simplifies DNS record management
- nslookup is critical for troubleshooting DNS issues

---

# Issues Encountered
- ICMP (ping) blocked by default firewall rules
- DNS resolution must be verified using nslookup instead
- Azure VM sizes weren't available in US-East so I had to create a new resource group and put it in US-East2

---
