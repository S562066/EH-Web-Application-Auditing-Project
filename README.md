# EH-Web-Application-Auditing-Project
Final project for Ethical Hacking 44481

Participants:  
Ash Atwell  
Abdul Moiz  
Carson Stockdale  

Introduction:  
OWASP Juice Shop is an application that contains many intentional vulnerabilities.   

Setup for Kali:  
Update your system: sudo apt update && sudo apt upgrade -y  
Install docker: sudo apt install docker.io -y   
To check version: sudo docker --version   
Download and run: sudo docker run -d -p 3000:3000 bkimminich/juice-shop    
     
To access juice shop, go to your browser and type: http://localhost:3000   


# XSS 

# Login via SQL Injection
### Description
In this part, I tested the login functionality of OWASP Juice Shop to check for SQL injection vulnerabilities. The goal was to see if the application properly validates user input.

### Payload Used
' OR 1=1 --

### Steps Performed
1. Opened the Juice Shop application in the browser
2. Navigated to the login page
3. Entered the SQL injection payload in the email field
4. Entered a random password
5. Clicked the login button

### Result
The application allowed login without valid credentials. This means the authentication system can be bypassed using SQL injection.

### Explanation
Normally, the system checks if the email and password match. However, the payload changed the query logic to always return true. Because of this, the system accepted the login without verifying real credentials.

### Impact
An attacker can gain unauthorized access to the system. This is a serious security issue because it exposes user accounts and sensitive data.

### Remediation
- Use parameterized queries (prepared statements)
- Avoid building SQL queries using string concatenation
- Validate user input on the server side
- Use proper error handling
<img width="1465" height="792" alt="success" src="https://github.com/user-attachments/assets/35da8c1c-2495-479f-ac28-5643e9aa70fa" />
<img width="1465" height="792" alt="payload" src="https://github.com/user-attachments/assets/31b3e199-d535-4c0d-ab33-8623fdc5d808" />
<img width="1465" height="792" alt="login failed" src="https://github.com/user-attachments/assets/54a975f7-25dc-4c67-813b-e47949e38734" />
<img width="1465" height="792" alt="login" src="https://github.com/user-attachments/assets/dc76a7e1-eb9b-4dbe-95c7-8b3d394d3d14" />
<img width="1465" height="792" alt="running" src="https://github.com/user-attachments/assets/dc341b97-a0f9-4f41-b21d-2fa8a540f34b" />

# Get Baskets
