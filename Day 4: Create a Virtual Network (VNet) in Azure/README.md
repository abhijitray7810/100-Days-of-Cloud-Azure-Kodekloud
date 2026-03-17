# Azure Virtual Network Setup - DevOps Migration Task
![image](https://github.com/abhijitray7810/100-Days-of-Cloud-Azure-Kodekloud/blob/9afc26169c88328616acc6da931ff348b613a458/Day%204%3A%20Create%20a%20Virtual%20Network%20(VNet)%20in%20Azure/Screenshot%202026-03-17%20173751.png)
## 📌 Project Overview

The Nautilus DevOps team is executing a phased migration of infrastructure to the Azure cloud. To ensure a smooth and low-risk transition, the migration is being performed incrementally by breaking down large tasks into smaller, manageable units.

This project demonstrates the creation of a foundational Azure networking component — a **Virtual Network (VNet)** — which serves as the backbone for cloud infrastructure.

---
![image](https://github.com/abhijitray7810/100-Days-of-Cloud-Azure-Kodekloud/blob/812961e33dcbbd21339af96e3320b7c666fcee3a/Day%204%3A%20Create%20a%20Virtual%20Network%20(VNet)%20in%20Azure/Screenshot%202026-03-17%20173809.png)
## 🎯 Objective

Create a Virtual Network named **`devops-vnet`** in the **Central US** region with a valid IPv4 CIDR block.

---

## 🏗️ Architecture Details

* **Virtual Network Name:** devops-vnet
* **Region:** Central US
* **Address Space:** 10.0.0.0/16
* **Subnet Name:** default
* **Subnet Range:** 10.0.0.0/24

---
![image]()
## ⚙️ Prerequisites

* Azure account access
* Azure CLI installed
* Valid credentials (provided in lab environment)

---

## 🚀 Implementation Steps
![image]()
### 1. Login to Azure

```bash
az login
```

---

### 2. Create Resource Group

```bash
az group create \
  --name devops-rg \
  --location centralus
```

---

### 3. Create Virtual Network

```bash
az network vnet create \
  --name devops-vnet \
  --resource-group devops-rg \
  --location centralus \
  --address-prefix 10.0.0.0/16 \
  --subnet-name default \
  --subnet-prefix 10.0.0.0/24
```

---

### 4. Verify Deployment

```bash
az network vnet list --output table
```

---

## ✅ Expected Outcome

* A Virtual Network named **devops-vnet** is successfully created
* The VNet is deployed in the **Central US** region
* The network includes a default subnet

---

## 💡 Key DevOps Concepts Applied

* Incremental Infrastructure Deployment
* Infrastructure as Code (CLI-based provisioning)
* Cloud Network Segmentation
* Scalable Architecture Design

---

## 📚 Future Enhancements

* Add Network Security Groups (NSG)
* Deploy Virtual Machines within the VNet
* Implement Load Balancer
* Design Hub-Spoke Network Architecture
* Automate using Terraform or ARM templates

---

## 🧑‍💻 Author

Abhijit Ray
DevOps & Cloud Enthusiast

---

## 📄 License

This project is for learning and demonstration purposes.
