# Nessus Vulnerability Scan on OWASP Juice Shop (Windows + Node.js)

This project demonstrates how to set up and run a complete vulnerability-scanning environment using OWASP Juice Shop (a deliberately insecure web application) and Nessus Essentials (a powerful vulnerability scanner). The goal is to provide a simple, hands-on introduction to web application security testing. You will learn how to install Juice Shop on Windows using Node.js, configure Nessus, perform unauthenticated scans, analyze vulnerability findings, and export reports.

------------------------------------------------------------------------

## 📌 Prerequisites

-   Windows 10/11
-   **Node.js LTS** installed → https://nodejs.org
-   At least **8 GB RAM**
-   A browser (Chrome/Edge/Firefox)
-   Nessus Essentials key (free)

------------------------------------------------------------------------

# 🚀 1. Install and Run OWASP Juice Shop (Windows + Node.js)

### **Step 1 --- Install Node.js**

Download and install Node.js from:
https://nodejs.org/en/download/prebuilt-installer

Verify installation:

``` cmd
node -v
npm -v
```

### **Step 2 --- Download Juice Shop**

``` cmd
git clone https://github.com/juice-shop/juice-shop.git
cd juice-shop
```

### **Step 3 --- Install Dependencies**

``` cmd
npm install
```

### **Step 4 --- Start Juice Shop**

``` cmd
npm start
```

Juice Shop will run by default on:

    http://localhost:3000

------------------------------------------------------------------------

# 🔐 2. Install Nessus Essentials (Windows)

### **Step 1 --- Download Nessus**

Download the Windows installer:
https://www.tenable.com/products/nessus/nessus-essentials

Choose:

    Nessus Essentials — Windows 64-bit

### **Step 2 --- Install Nessus**

Run the installer → it starts Nessus service automatically.

### **Step 3 --- Open Nessus in Browser**

Go to:

    https://localhost:8834/

### **Step 4 --- Register Nessus**

Choose: - **Nessus Essentials (Free)** - Enter activation code (sent via
email)

### **Step 5 --- Allow Plugin Compilation**

Compilation takes: - **5--20 minutes**, depending on PC

Wait until **"Plugins compiled successfully"**.

------------------------------------------------------------------------

# 🕵️‍♂️ 3. Create a Nessus Scan for Juice Shop

### **Step 1 --- Create New Scan**

1.  Go to **Scans**
2.  Click **New Scan**
3.  Choose **Basic Network Scan**

### **Step 2 --- Configure Target**

In **Targets** field enter:

    http://localhost:3000
    127.0.0.1

### **Step 3 (Optional) --- Disable Credential Requirements**

Juice Shop is intentionally insecure, so we do:

Go to: **Advanced → Scan Type → Unauthenticated**

### **Step 4 --- Save & Launch**

Click **Save**\
Then click **Launch**

------------------------------------------------------------------------

# 📊 4. Reviewing Scan Results

After scan completes: - Open the scan - View **Vulnerabilities** - Sort
by: - Critical - High - Medium

You'll see issues such as: - Cross‑site scripting (XSS) - SQL
injection - Sensitive data exposure - Components with known
vulnerabilities

------------------------------------------------------------------------

