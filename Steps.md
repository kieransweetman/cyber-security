
# **1. Testing with Metasploit**

#### **Step 1: Authentication Endpoint (`http://localhost:9898/`)**

- Launch Metasploit:  
    Run `msfconsole` in your terminal.
    
- Identify vulnerabilities:
    
    - Use the `auxiliary/scanner/http/http_login` module.
    - Set the target URL (`RHOSTS`) to `localhost` and the port (`RPORT`) to `9898`.
    - Configure a dictionary attack or brute force to test the login.

- Add user to the database:
    
    - Manually insert a new user into your database table (`User`) with a username and password.
    - Re-test login functionality with the newly added credentials.


#### Results

![[methodology]]

---

# **2. Testing API Endpoints**

#### **Step 2.1: Testing `/api/clients`**

- Use the Metasploit `auxiliary/scanner/http/http_version` module to enumerate information about the API endpoint.
- Check if it exposes any sensitive data or misconfigurations.

#### **Step 2.2: Testing `/client/add`**

- Explore if the endpoint is vulnerable to injection attacks:
    - Use the `auxiliary/scanner/http/sql_injection` module from Metasploit.
    - Analyze the results to determine if the endpoint can be exploited for SQL injection.

---

# **3. Testing with SQLMap**

#### **Step 3.1: Testing `/api/clients`**

- Run SQLMap:
    
    lua
    
    Copy code
    
    `sqlmap -u "http://localhost:9898/api/clients" --batch`
    
- Check for vulnerabilities like SQL injection.

#### **Step 3.2: Testing `/client/add`**

- If this endpoint requires POST data, run SQLMap as follows:
    
    kotlin
    
    Copy code
    
    `sqlmap -u "http://localhost:9898/client/add" --data="param1=value1&param2=value2" --batch`
    

---

# **4. Conducting a Penetration Test**

- **Goal:** Simulate real-world attack scenarios and find weaknesses.
- Use the following tools:
    - **Burp Suite**: To intercept and manipulate HTTP requests for deeper testing.
    - **Metasploit**: To attempt exploitation using modules based on discovered vulnerabilities.
    - **SQLMap**: For SQL injection testing.

#### Suggested Steps:

1. Map the application:
    - Identify all endpoints and understand their functionality.
2. Exploit common vulnerabilities:
    - Test for SQL injection, XSS, CSRF, and authentication bypass.
3. Generate a report:
    - Document findings, exploited vulnerabilities, and recommended fixes.