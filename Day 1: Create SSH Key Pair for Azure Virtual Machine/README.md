# Azure SSH Key Pair Creation - Task Documentation
![image](https://github.com/abhijitray7810/100-Days-of-Cloud-Azure-Kodekloud/blob/a2dade0663ddedeaf8647818228084517672b4ba/Day%201%3A%20Create%20SSH%20Key%20Pair%20for%20Azure%20Virtual%20Machine/Screenshot%202026-02-02%20120130.png)
## Overview
This document provides a comprehensive guide for creating an SSH key pair in Azure as part of the Nautilus DevOps team's incremental cloud migration strategy.

## Task Objective
Create an SSH key pair in Azure with specific requirements to support the infrastructure migration process.

## Requirements
![image](https://github.com/abhijitray7810/100-Days-of-Cloud-Azure-Kodekloud/blob/a2dade0663ddedeaf8647818228084517672b4ba/Day%201%3A%20Create%20SSH%20Key%20Pair%20for%20Azure%20Virtual%20Machine/Screenshot%202026-02-02%20120142.png)
### SSH Key Pair Specifications
- **Name**: `xfusion-kp`
- **Key Type**: RSA
- **Purpose**: Enable secure authentication for Azure resources during migration

### Azure Credentials
- **Portal URL**: https://portal.azure.com
- **Username**: `kk_lab_user_main-8aad9b588be9457c@azurefreekmlprod.onmicrosoft.com`
- **Password**: `&^B+98EL`
- **Access Window**: Mon Feb 02 06:23:39 UTC 2026 - Mon Feb 02 07:23:39 UTC 2026

## Implementation Steps
![image](https://github.com/abhijitray7810/100-Days-of-Cloud-Azure-Kodekloud/blob/a2dade0663ddedeaf8647818228084517672b4ba/Day%201%3A%20Create%20SSH%20Key%20Pair%20for%20Azure%20Virtual%20Machine/Screenshot%202026-02-02%20120200.png)
### Method 1: Azure Portal (GUI)

1. **Login to Azure Portal**
   - Navigate to https://portal.azure.com
   - Enter the provided credentials
   - Complete authentication

2. **Navigate to SSH Keys Service**
   - In the Azure Portal search bar, type "SSH keys"
   - Select "SSH keys" from the services list
   - Or navigate via: Home → All Services → Compute → SSH keys

3. **Create New SSH Key Pair**
   - Click "+ Create" button
   - Fill in the required information:
     - **Subscription**: Select your subscription
     - **Resource Group**: Select existing or create new
     - **Region**: Choose appropriate region
     - **Key pair name**: `xfusion-kp`
     - **SSH public key source**: Generate new key pair
     - **Key type**: RSA

4. **Generate and Download**
   - Click "Review + Create"
   - Review the configuration
   - Click "Create"
   - **Important**: Download the private key immediately (it's only available once)
   - The private key will be downloaded as `xfusion-kp.pem`

5. **Verification**
   - Navigate to SSH keys in Azure Portal
   - Verify `xfusion-kp` appears in the list
   - Note the resource group and region

### Method 2: Azure CLI

```bash
# Login to Azure
az login -u kk_lab_user_main-8aad9b588be9457c@azurefreekmlprod.onmicrosoft.com

# Set variables
RESOURCE_GROUP="your-resource-group"
KEY_NAME="xfusion-kp"
REGION="eastus"  # or your preferred region

# Create SSH key pair
az sshkey create \
  --name $KEY_NAME \
  --resource-group $RESOURCE_GROUP \
  --location $REGION

# Verify creation
az sshkey list --resource-group $RESOURCE_GROUP --output table
```

### Method 3: Azure PowerShell

```powershell
# Connect to Azure
Connect-AzAccount -UserName "kk_lab_user_main-8aad9b588be9457c@azurefreekmlprod.onmicrosoft.com"

# Set variables
$ResourceGroup = "your-resource-group"
$KeyName = "xfusion-kp"
$Location = "eastus"  # or your preferred region

# Create SSH key pair
New-AzSshKey -ResourceGroupName $ResourceGroup -Name $KeyName -Location $Location

# Verify creation
Get-AzSshKey -ResourceGroupName $ResourceGroup
```

## Post-Creation Tasks
![image](https://github.com/abhijitray7810/100-Days-of-Cloud-Azure-Kodekloud/blob/a2dade0663ddedeaf8647818228084517672b4ba/Day%201%3A%20Create%20SSH%20Key%20Pair%20for%20Azure%20Virtual%20Machine/Screenshot%202026-02-02%20120218.png)
### Secure the Private Key

1. **Set Proper Permissions** (Linux/Mac)
   ```bash
   chmod 600 xfusion-kp.pem
   ```

2. **Store Securely**
   - Keep the private key in a secure location
   - Consider using Azure Key Vault for centralized secret management
   - Never commit private keys to version control
   - Create backup copies in secure storage

3. **Document Location**
   - Record where the private key is stored
   - Document who has access
   - Maintain access control policies

### Using the SSH Key
![image](https://github.com/abhijitray7810/100-Days-of-Cloud-Azure-Kodekloud/blob/a2dade0663ddedeaf8647818228084517672b4ba/Day%201%3A%20Create%20SSH%20Key%20Pair%20for%20Azure%20Virtual%20Machine/Screenshot%202026-02-02%20120318.png)
**Connect to Azure VM:**
```bash
ssh -i xfusion-kp.pem azureuser@<vm-ip-address>
```

**Specify in Azure VM Creation:**
- When creating a new VM, select "Use existing key stored in Azure"
- Choose `xfusion-kp` from the dropdown

## Verification Checklist

- [ ] SSH key pair `xfusion-kp` created in Azure
- [ ] Key type is RSA
- [ ] Private key downloaded and secured (chmod 600)
- [ ] Public key visible in Azure Portal
- [ ] Key is available in the correct resource group
- [ ] Access documented and controlled
- [ ] Backup of private key created (if applicable)

## Migration Strategy Context

This SSH key pair creation is part of a larger incremental migration strategy:

### Phase Approach
1. **Infrastructure Preparation** (Current Phase)
   - Create authentication mechanisms (SSH keys)
   - Set up networking components
   - Configure security groups

2. **Resource Migration**
   - Migrate workloads incrementally
   - Use SSH keys for secure access
   - Validate each migration step

3. **Optimization**
   - Fine-tune configurations
   - Implement automation
   - Monitor and adjust

### Benefits of Incremental Approach
- **Risk Mitigation**: Smaller changes reduce impact of potential issues
- **Better Control**: Easier to track and manage individual components
- **Resource Optimization**: Efficient use of team time and cloud resources
- **Minimal Disruption**: Ongoing operations continue with minimal interruption

## Troubleshooting

### Common Issues

**Issue**: Cannot find SSH Keys in Azure Portal
- **Solution**: Ensure you're logged into the correct subscription and have proper permissions

**Issue**: Private key download failed
- **Solution**: The private key is only available once during creation. You'll need to create a new key pair if lost

**Issue**: Permission denied when using SSH key
- **Solution**: Check file permissions (`chmod 600`) and ensure you're using the correct key file

**Issue**: Key not appearing in VM creation wizard
- **Solution**: Ensure the key is in the same region as the VM you're creating, or use a different region

## Security Best Practices

1. **Key Rotation**: Plan to rotate SSH keys periodically
2. **Access Control**: Limit who has access to private keys
3. **Monitoring**: Enable Azure Monitor to track SSH key usage
4. **Multi-Factor Authentication**: Use MFA for Azure Portal access
5. **Audit Logging**: Review Azure Activity Logs regularly

## Additional Resources

- [Azure SSH Keys Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/ssh-keys-portal)
- [Azure CLI SSH Key Commands](https://docs.microsoft.com/en-us/cli/azure/sshkey)
- [SSH Best Practices](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed)

## Task Completion

**Task Status**: ✅ Completed

**Completed By**: Nautilus DevOps Team  
**Completion Date**: Mon Feb 02, 2026  
**Key Name**: xfusion-kp  
**Key Type**: RSA  

---

## Notes

- This is the first task in the Azure migration journey
- Future tasks will build upon this foundation
- Document any deviations or additional configurations
- Update this README as the migration progresses

## Next Steps

1. Create Azure Virtual Network
2. Set up Resource Groups
3. Deploy test VM using the SSH key
4. Implement monitoring and logging
5. Begin application migration

---

*This documentation is part of the Nautilus DevOps team's Azure cloud migration initiative.*
