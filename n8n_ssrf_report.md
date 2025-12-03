# Title：SSRF Vulnerability in the "Import from URL" Function of n8n System

## 1.summary

- Title：SSRF Vulnerability in the "Import from URL" Function of n8n System

- Vendor：n8n

- Product:n8n

- Affected Versions:all

- Vulnerability Type: SSRF

## 2.Vulnerability Details

### 2.1Description

The "Import from URL" feature in n8n's workflow contains a **Server-Side Request Forgery (SSRF) vulnerability**. By constructing malicious URL parameters, an attacker can force the server to send requests to internal networks or protected systems. This allows them to bypass firewall restrictions, access internal services, or perform sensitive operations.

### 2.2Proof of Concept (PoC)

- Step 1: Deploy the n8n system using Docker 

```docker volume create n8n_data```

 ```docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n```

 ```docker.n8n.io/n8nio/n8n ``` 

Step 2: After creating an account and logging in, click to create a workflow 
![1siginin]（1siginin.png）
![2createworkflow]（2createworkflow.png）

Step 3:   Click "Add Node" and select "Trigger manually" 
![3.1trigger]（3.1trigger.png）

Step 4: Click the ellipsis icon in the top right corner and Choose "Import from URL" 
![3importURL]（3importURL.png）
Step 5: Enter `http://dnslog.com` in the URL field 

![4ssrftest]（4ssrftest.png）
Step 6: The dnslog platform receives the request
![5burpsuitesuccess]（5burpsuitesuccess.png）
![6hostip]（6hostip.png）
