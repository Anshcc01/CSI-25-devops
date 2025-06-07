
# Azure Hands-On Tasks - Step-by-Step Guide

## 1. Observe Assigned Subscriptions & Azure Entra ID

### Steps:
- Login to [Azure Portal](https://portal.azure.com)
- Navigate to **Subscriptions** under “All Services” to view assigned subscriptions
- Go to **Azure Entra ID** (formerly Azure AD) to observe or create directory

### Resources:
- [Azure Subscriptions Explained](https://www.youtube.com/watch?v=-BD5rlMyLUY)
- [Azure CLI Introduction](https://learn.microsoft.com/en-us/cli/azure/what-is-azure-cli)

---

## 2. Create Test Users and Groups in Azure Entra ID

### Steps:
- Go to **Azure Entra ID > Users > New User**
- Add user details and create
- For Groups: Azure Entra ID > Groups > New Group

---

## 3. Assign an RBAC Role to User and Test

### Steps:
- Go to any resource (e.g., VM or Resource Group)
- Click **Access Control (IAM)** > **Add role assignment**
- Choose role (e.g., Reader), select user, assign

---

## 4. Create and Assign Custom Role

### Steps:
- Azure Portal > Subscriptions > Access Control (IAM) > Roles > + Add Custom Role
- Define name, permissions JSON, assign to user

---

## 5. Create Virtual Machine and VNet via Azure CLI

### Steps:
```bash
az group create --name MyResourceGroup --location eastus
az network vnet create --name MyVnet --resource-group MyResourceGroup --subnet-name MySubnet
az vm create --resource-group MyResourceGroup --name MyVM --vnet-name MyVnet --subnet MySubnet --image UbuntuLTS --admin-username azureuser --generate-ssh-keys
```

### Resources:
- [Azure CLI VM and VNet](https://www.youtube.com/watch?v=DOywwse_j8I)
- [Azure PowerShell Docs](https://learn.microsoft.com/en-us/powershell/azure/what-is-azure-powershell?view=azps-9.3.0)

---

## 6. Create and Assign Policy at Subscription Level

### Steps:
- Azure Portal > Policy > Assign Policy
- Choose built-in or custom policy
- Set scope to subscription
- Assign and validate compliance

### Resources:
- [Azure Policy Explained](https://www.youtube.com/watch?v=4wGns611G4w)
- [ARM Templates Overview](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview)

---

## 7. Create Azure Key Vault and Store Secrets

### Steps:
```bash
az keyvault create --name MyKeyVault --resource-group MyResourceGroup --location eastus
az keyvault secret set --vault-name MyKeyVault --name MySecret --value "MyValue"
az keyvault secret show --name MySecret --vault-name MyKeyVault
```

### Resources:
- [Azure Key Vault Tutorial](https://www.youtube.com/watch?v=JDRixckApxM)

---

## 8. Create a VM Using PowerShell

### Resources:
- [Azure PowerShell VM](https://www.youtube.com/watch?v=-SRk0hHa-S0)

---

## 9. Schedule Daily VM Backup & Alert Rule

### A. Backup VM Daily at 3:00 AM:
- Azure Portal > Recovery Services Vault > Backup
- Choose VM, define policy (schedule, retention), enable backup

### B. Alert Rule for CPU > 80%:
- VM > Monitoring > Alerts > New Alert Rule
- Set condition: CPU % > 80
- Action: Email notification

### Resources:
- [Backup & Alerts](https://www.youtube.com/watch?v=lzVQ3NqMnTE)
- [Backup Policy & Retention](https://www.youtube.com/watch?v=A0jAeGf2zUQ)

---

## 10. Provision Backup from Backup Center

### Steps:
- Azure Portal > Backup Center > +Backup
- Configure the backup as above with policy and retention settings
