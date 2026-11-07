# Lab 02: Unprotected admin functionality with unpredictable URL

Difficulty: Apprentice\
Lab URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-unprotected-admin-functionality-with-unpredictable-url \
Vulnerability: Broken Access Control (CWE-862)\
Tools: Chrome Developer Tools\
Status: Solved

## Lab Description

This lab has an unprotected admin panel. It's located at an unpredictable location, but the location is disclosed somewhere in the application.

Solve the lab by accessing the admin panel, and using it to delete the user `carlos`.

## Discovery and Exploitation

### Step 1: Identify the Admin Endpoint
I opened the web application and used Chrome Developer Tools (Network → Response) to inspect the HTML response. Within the client-side JavaScript, I identified the administrative endpoint /admin-il1il3.

Although the administrative link was hidden from regular users, its endpoint remained visible in the application's source code.

### Step 2: Access the Admin Panel

I appended the discovered endpoint to the application's base URL and was able to access the admin panel without administrator privileges.

The panel displayed a list of users and provided the option to delete accounts.

### Step 3: Validate the Vulnerability
I used the admin panel to delete the test user carlos.

The application confirmed that the user was deleted, demonstrating that the admin panel and its account deletion functionality lacked proper authorization checks.

## Root Cause and Impact
The application did not enforce server-side authorization checks to verify whether users had permission to access the admin panel.

Although the admin link was hidden from the user interface, anyone who discovered the URL could access the panel.

An unauthorized user could access the admin panel and delete user accounts. In a real-world application, this could lead to unauthorized account changes, data loss, or disruption to users.

## Recommended Remediation
- Enforce server-side authorization: Check that users have administrator privileges before allowing access to the admin panel or performing administrative actions.

- Deny unauthorized requests: Block users without the required permissions, even if they know the admin URL.

- Validate access controls: Test both the administrative interface and its underlying endpoints to ensure unauthorized users cannot perform privileged actions.

## Key Takeaway
Hiding an administrative endpoint does not provide access control. Even when an administrative URL is difficult to discover, the application must enforce server-side authorization to prevent unauthorized access and privileged operations.

Hiding an admin panel or using an unpredictable URL does not make it secure. The application must enforce server-side authorization to ensure only users with the correct permissions can access administrative functionality.