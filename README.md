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

<pre> ```mermaid flowchart LR subgraph RG["Resource Group"] subgraph VNet["Virtual Network: CoreServicesVNet"] VM1["TestVM1"] VM2["TestVM2"] end end DNS["Private DNS Zone: contoso.com"] VM1 -- "Query" --> DNS DNS -- "Response" --> VM1 VM2 -- "DNS Query" --> DNS DNS -- "Response" --> VM2 VNet ---|"VNet Link"| DNS ``` </pre>



# Implementation Steps

# 1. Create Private DNS Zone
Name: contoso.com
Resource Group: ContosoResourceGroup

<img width="1363" height="473" alt="image" src="https://github.com/user-attachments/assets/5bd7e3a1-f892-4fd8-aaf0-b575dadd5539" />


Figure 1: Contoso.com Private DNS Zone created

---
# 2. Link Virtual Network
VNet: CoreServicesVnet
Auto-registration: Enabled

<img width="1570" height="445" alt="image" src="https://github.com/user-attachments/assets/c012621f-af61-4b50-9e8d-791867cade61" />


Figure 2: Virtual network linked to private DNS zone

---

# 3. Deploy Virtual Machines
```
$RGName = "ContosoResourceGroup"

New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateFile azuredeploy.json -TemplateParameterFile azuredeploy.parameters.json

```

<img width="1757" height="383" alt="image" src="https://github.com/user-attachments/assets/28306428-7e47-4624-91f4-af07839e4d9c" />


Figure 3: Virtual machines deployed

<img width="1369" height="578" alt="image" src="https://github.com/user-attachments/assets/5cf83a4c-7bea-4304-aaff-92bd048b1b9c" />


Figure 4: Virtual machine DNS records

---

# 4. Verify DNS Resolution
```
nslookup TestVM2.contoso.com
```

<img width="447" height="197" alt="image" src="https://github.com/user-attachments/assets/9bb9a263-b3ab-4021-8778-8194edd961ec" />


Figure 5: Internal hostname successfully resolved

---

# Key Learnings
- Private DNS Zones enable secure internal name resolution
- Auto-registration simplifies DNS record management

---

# Issues Encountered
- ICMP (ping) blocked by default firewall rules
- DNS resolution must be verified using nslookup instead
- Azure VM sizes weren't available in US-East so I had to create a new resource group and put it in US-East2

---
