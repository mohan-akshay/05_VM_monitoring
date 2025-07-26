# 📈 Azure VM Monitoring & Alerts

## 📝 Summary

This project demonstrates how to configure **Azure Monitor** to track CPU usage of a virtual machine (VM) and trigger **email alerts** when usage exceeds a threshold. This hands-on exercise helps in understanding Azure's monitoring capabilities and proactive alerting for system health and performance.

---

## 📘 Topics Covered

- Azure Linux VM provisioning
- Azure Monitor metrics and alert rules
- Creating action groups for alert notifications
- Simulating high CPU usage
- Validating email-based alerts
- Resource cleanup

---

## 💡 Scenario

A system administrator needs to monitor a virtual machine's performance and get notified if the CPU usage spikes. This is essential in production environments where resource exhaustion could impact application availability.

You'll simulate this by creating a Linux VM, monitoring CPU usage, and setting up an alert rule to email you if CPU usage exceeds 80% for over 5 minutes.

---

## ⚙️ Step-by-Step Guide

### 1. 🖥️ Create a Linux VM

1. Go to: `Azure Portal → Virtual Machines → + Create`
2. Fill in the details:
   - **Resource Group**: `az900-project5-rg` *(create if not existing)*
   - **VM Name**: `az900monitorvm`
   - **Region**: Choose your preferred Azure region
   - **Image**: Ubuntu LTS (e.g., Ubuntu 20.04)
   - **Size**: Use a basic SKU like `B1s`
   - **Authentication type**: Password or SSH public key
3. Click **Review + create** → **Create**

---

### 2. 📊 Enable Azure Monitor Metrics

1. After the VM is deployed, go to: `Virtual Machines → az900monitorvm`
2. In the left menu, scroll down to **Monitoring → Metrics**
3. Click **+ Add metric**
   - Select **Metric namespace**: `Virtual Machine Host`
   - Choose **Metric**: `Percentage CPU`
   - Review the CPU usage over time

---

### 3. 🚨 Create a CPU Alert Rule

1. Go to: `Virtual Machines → az900monitorvm → Alerts → + Create → Alert rule`
2. Set up the **condition**:
   - Click **Add condition** → Choose **Percentage CPU**
   - Operator: **Greater than**
   - Threshold value: `80`
   - Aggregation: `Average`
   - Frequency: **Over the last 5 minutes**
3. Create an **Action Group**:
   - Click **Add action group**
   - Name: `AZ900-Admin-Alerts`
   - Short name: `admin`
   - **Notifications** tab → Add your email under Email/SMS/Push/Voice
   - Click **Review + create** → Create action group
4. Set **Alert rule name**: `High-CPU-Alert`
5. Click **Review + create** → **Create**

---

### 4. 🧪 Simulate High CPU Usage

1. **SSH into the VM** from Azure Cloud Shell or terminal:
   ```
   ssh <your-vm-username>@<public-ip-address>
   ```
2. Install the stress tool:
```
sudo apt-get update && sudo apt-get install -y stress-ng
```

3. Generate high CPU load for 5 minutes:
```
stress-ng --cpu 1 --timeout 300s
```

---

### 5. 📥 Check for Alerts

- Wait about **5–10 minutes** after generating CPU load.
- You should receive an **email notification** at the address you provided in the action group.
- You can also view the triggered alert from the Azure portal: Azure Portal → Virtual Machines → az900monitorvm → Alerts → Alert rules

---

### 6. 🧹 Cleanup

To avoid unnecessary charges:

1. Go to: **Azure Portal → Resource groups**
2. Select the resource group: `az900-project5-rg`
3. Click **Delete resource group**
4. Confirm the resource group name to permanently remove all related resources

---

### 🌐 Tools & Services Used
- Azure Virtual Machines
- Azure Monitor
- Azure Alerts & Action Groups
- Linux Terminal / SSH
- stress-ng tool (for CPU simulation)

---

### 🎯 Outcome
Got hands-on experience with:
- Monitoring real-time VM metrics in Azure
- Creating automated alert rules with email notifications
- Simulating high CPU load on a Linux VM
- Managing and cleaning up Azure resources effectively

