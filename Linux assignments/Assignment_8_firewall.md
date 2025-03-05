# Assignment 8 - Linux Firewall Report
## Student Name
Milan Khadka 
## **1. Introduction**  
A firewall is a critical component in securing network services on a Linux server. In this report, I configure a firewall using `iptables` (or `ufw` as an alternative) to protect the following services:  

- **OpenSSH Server** (for remote administration)  
- **HTTP and HTTPS Servers** (for web hosting)  

Additionally, I implement logging mechanisms for allowed and blocked connections and set up protection against **SYN flood attacks** and at least one additional common attack.

---

## **2. Firewall Setup on Linux**  

### **2.1 Install and Enable Firewall**  

I will use `iptables` for fine-grained control. To install and enable it, run:  

```bash
sudo apt update && sudo apt install iptables-persistent -y
```

Ensure `iptables` runs on startup:  

```bash
sudo systemctl enable netfilter-persistent
```

Alternatively, if using **`ufw` (Uncomplicated Firewall)**, enable it with:

```bash
sudo apt install ufw -y
sudo ufw enable
```

---

## **3. Firewall Rules Configuration**  

### **3.1 Allow Essential Services**  

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT   # Allow SSH  
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT   # Allow HTTP  
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT  # Allow HTTPS  
```

If using `ufw`, apply the following:

```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

---

### **3.2 Block and Log Unauthorized Traffic**  

#### **Block All Other Incoming Traffic and Log It**  

```bash
sudo iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables-blocked: " --log-level 4
sudo iptables -A INPUT -j DROP
```

---

### **3.3 Protection Against SYN Flood Attacks**  

SYN flood attacks exploit the TCP handshake by overwhelming the system with half-open connections. We mitigate this by:  

```bash
sudo iptables -A INPUT -p tcp --syn -m limit --limit 1/s --limit-burst 3 -j ACCEPT
```

This rule limits SYN packets to **one per second**, with a burst of three.  

---

### **3.4 Additional Attack Prevention: Ping Flood**  

A **Ping flood (ICMP flood)** can exhaust system resources. To limit ICMP requests:  

```bash
sudo iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s --limit-burst 3 -j ACCEPT
```

---

## **4. Saving and Applying Firewall Rules**  

To ensure rules persist after reboot:  

```bash
sudo netfilter-persistent save
sudo netfilter-persistent reload
```

For `ufw`, reload rules with:  

```bash
sudo ufw reload
```

---

## **5. Conclusion**  

With this configuration:  
- SSH, HTTP, and HTTPS services are accessible.  
-  Unauthorized traffic is logged and blocked.  
- Protection is enabled against **SYN flood** and **ICMP flood** attacks.  

This firewall setup significantly enhances server security while allowing essential services to operate. 

---

