# Lab: Basic SSRF against the local server

**Platform:** PortSwigger Web Security Academy  
**Category:** Server-Side Request Forgery (SSRF)

---

### 📝 Summary
The stock check feature on the website accepts a user-provided URL and makes a request to it from the server. Because the request originates from the internal network, we can use it to reach internal systems that aren't exposed to the public internet.

### 🚀 Steps

1. **Intercept:** Captured the `stockApi` request in Burp Suite Proxy.
2. **Modify:** Replaced the target URL with the internal admin panel address: `http://192.168.0.1:8080/admin`.
3. **Bruteforce:** Sent the request to Burp Intruder and set the final IP octet (the `1` in `192.168.0.1`) as the payload position.
4. **Attack:** Configured a numeric payload list (`1–255`, step `1`) and started the attack.
5. **Identify:** Sorted the Intruder results by status code. Found a single `200 OK` response pointing to the internal admin interface.
6. **Exploit:** Sent that successful request to Burp Repeater and changed the path to: 
   `/admin/delete?username=carlos`

### ✅ Result
**Lab solved!** The admin interface was successfully reached via SSRF, and the target user (`carlos`) was deleted.

### 💥 Impact
An attacker could use this SSRF flaw to access internal admin panels and backend systems that are not exposed to the internet. In a real-world scenario, this could lead to full system compromise, data theft, or unauthorized actions on the server.

### 🛠️ Tools Used
*   Burp Suite (Proxy, Intruder, Repeater)