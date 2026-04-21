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

In this part, I tested the login functionality of OWASP Juice Shop to check for SQL injection vulnerabilities. The goal was to determine whether the application properly validates and handles user input during authentication.

### Payload Used

`' OR 1=1 --`

### Steps Performed

1. Opened the OWASP Juice Shop application in the browser  
2. Navigated to the login page  
3. Entered the SQL injection payload in the email field  
4. Entered a random value in the password field  
5. Submitted the login form  

### Result

The application allowed login without valid credentials. This confirms that the authentication mechanism is vulnerable to SQL injection and can be bypassed.

### Explanation

Normally, the application checks whether the email and password entered by the user match the records stored in the database. However, when the payload `' OR 1=1 --` is entered, it changes the logic of the SQL query.

Instead of checking for a specific user, the condition becomes true for all records because `1=1` is always true. The `--` symbol comments out the rest of the query, so the password check is ignored. As a result, the system grants access without verifying real credentials.

### Impact

This vulnerability allows an attacker to bypass authentication and gain unauthorized access to the application. It can lead to exposure of user data, account takeover, and further exploitation of the system. This is considered a high severity security issue.

### Remediation

The vulnerability occurs because user input is directly inserted into SQL queries without proper handling.

To fix this issue:

- Use parameterized queries (prepared statements) so that user input is treated strictly as data and not executable SQL  
- Avoid building SQL queries using string concatenation, as this allows attackers to inject malicious input  
- Validate and sanitize all user inputs on the server side to ensure they follow expected formats  
- Implement proper error handling so sensitive database errors are not exposed to users  
- Apply least-privilege database access to minimize potential damage if an attack occurs  

### Example Fix

Vulnerable approach:
`SELECT * FROM users WHERE email = 'user_input' AND password = 'password'`


This directly inserts user input into the SQL query.

Secure approach:
`SELECT * FROM users WHERE email = ? AND password = ?`


In this version, placeholders are used and the input is passed separately. This ensures that the database treats the input as plain data instead of SQL code, preventing injection attacks.

### Screenshots

![success](https://github.com/user-attachments/assets/35da8c1c-2495-479f-ac28-5643e9aa70fa){style="width: 1465; height: 792;"}
![payload](https://github.com/user-attachments/assets/31b3e199-d535-4c0d-ab33-8623fdc5d808){style="width: 1465; height: 792;"}
![login failed](https://github.com/user-attachments/assets/54a975f7-25dc-4c67-813b-e47949e38734){style="width: 1465; height: 792;"}
![login](https://github.com/user-attachments/assets/dc76a7e1-eb9b-4dbe-95c7-8b3d394d3d14){style="width: 1465; height: 792;"}
![running](https://github.com/user-attachments/assets/dc341b97-a0f9-4f41-b21d-2fa8a540f34b){style="width: 1465; height: 792;"}

# Get Baskets

## Description

In this section we tested the access control of the user's basket data. The
intention was to see if there is any way to fetch data that does not belong to
the requesting user.
