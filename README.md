<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# **Network Security Groups (NSGs) and Analyzing Traffic Between Azure Virtual Machines**
This guide explores how to inspect network traffic between **Azure Virtual Machines** using **Wireshark** and demonstrates the role of **Network Security Groups (NSGs)** in managing network security.

---

## **Environments and Technologies Used**
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Protocol (RDP)
- Windows and Linux Command Line Utilities
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Packet Analyzer)

---

## **Operating Systems Used**
- Windows 10 (21H2)
- Ubuntu Server 22.04

---

## **Steps and Observations**

### **Step 1: Deploying Virtual Machines in Azure**
<p>
<img src="https://i.imgur.com/EwX8Y7s.png" alt="Azure VM Deployment"/>
<img src="https://i.imgur.com/JGhlxJJ.png" alt="VM Configuration"/>
</p>
- Set up two **Azure Virtual Machines**:
  - One running **Windows 10 Pro**
  - Another running **Ubuntu Server**
- Ensure both VMs are linked to the same **virtual network (VNet)** to facilitate communication.
- Use **RDP** to connect to the **Windows VM**.

---

### **Step 2: Installing Wireshark for Network Analysis**
<p>
<img src="https://i.imgur.com/1BYvdJZ.png" alt="Wireshark Setup"/>
</p>
- Download and install **Wireshark** from [Wireshark.org](https://www.wireshark.org).
- Open **Wireshark** to begin monitoring network activity.

---

### **Step 3: Monitoring ICMP Traffic in Wireshark**
<p>
<img src="https://i.imgur.com/3gTUIDW.png" alt="ICMP Traffic Monitoring"/>
</p>
- Within **Wireshark**, apply a filter to view only **ICMP traffic**.
- **ICMP (Internet Control Message Protocol)** is often used for connectivity testing and error reporting.

---

### **Step 4: Testing Network Connectivity with Ping**
<p>
<img src="https://i.imgur.com/HgLp5AR.png" alt="Ping Test Execution"/>
</p>
- Launch **PowerShell** on the **Windows VM**.
- Run the `ping` command to check connectivity with the **Linux VM** using its **private IP address**.
- The **Linux VM’s private IP** can be found in **Azure Portal > VM Network Settings**.

---

### **Step 5: Capturing ICMP Traffic in Wireshark**
<p>
<img src="https://i.imgur.com/nurPwTN.png" alt="ICMP Packet Capture"/>
</p>
- View real-time **ICMP traffic** in **Wireshark** while pinging the Linux machine.

---

### **Step 6: Blocking ICMP Traffic in NSGs**
<p>
<img src="https://i.imgur.com/X4yfgee.png" alt="Blocking ICMP in Network Security Group"/>
</p>
- Execute `ping -t` to generate continuous ping requests.
- In **Azure**, configure the **Network Security Group (NSG)** to **block ICMP traffic**.

---

### **Step 7: Confirming ICMP Traffic Block**
<p>
<img src="https://i.imgur.com/UvdXvva.png" alt="Blocked ICMP Traffic"/>
</p>
- Verify in **Wireshark** that responses to ping requests have stopped.
- Observe the `"Request Timed Out"` message in **PowerShell**.

---

### **Step 8: Restoring ICMP Traffic**
<p>
<img src="https://i.imgur.com/QstVuqS.png" alt="Restoring ICMP Traffic"/>
</p>
- Remove the **NSG inbound rule** that blocks ICMP.
- Stop continuous pinging by pressing **Ctrl + C** in PowerShell.

---

### **Step 9: Capturing SSH Traffic in Wireshark**
<p>
<img src="https://i.imgur.com/5sVds9j.png" alt="SSH Traffic Analysis"/>
</p>
- Filter **Wireshark** for **SSH traffic**.
- Connect to the **Linux VM** from **Windows** using SSH:
  ```bash
  ssh labuser2@10.0.0.5
  ```
- Observe **SSH packets** in **Wireshark**.
- Use `exit` to close the SSH session.

---

### **Step 10: Examining DNS Traffic in Wireshark**
<p>
<img src="https://i.imgur.com/WlKABeY.png" alt="DNS Query Analysis"/>
</p>
- Configure **Wireshark** to display **DNS traffic**.
- Generate a DNS query in PowerShell:
  ```bash
  nslookup www.yahoo.com
  ```
- Observe the **DNS request and response** in **Wireshark**.

---

### **Step 11: Monitoring DHCP Traffic in Wireshark**
<p>
<img src="https://i.imgur.com/afL911f.png" alt="DHCP Traffic Analysis"/>
</p>
- **DHCP (Dynamic Host Configuration Protocol)** assigns IP addresses dynamically.
- Force a DHCP lease renewal using PowerShell:
  ```bash
  ipconfig /renew
  ```
- Capture the **DHCP request and response packets** in **Wireshark**.

---

### **Step 12: Observing RDP Traffic in Wireshark**
<p>
<img src="https://i.imgur.com/KUhVqBe.png" alt="RDP Traffic Capture"/>
</p>
- **RDP (Remote Desktop Protocol)** facilitates VM management in Azure.
- Analyze **continuous RDP traffic** in **Wireshark** while connected.

---

## **Conclusion**
By following this guide, you can analyze network traffic between **Azure Virtual Machines** using **Wireshark** and gain insights into how **NSGs** play a crucial role in securing cloud-based networking environments.
