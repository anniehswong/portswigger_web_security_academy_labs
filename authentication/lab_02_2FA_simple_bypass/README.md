# Lab 02: 2FA simple bypass

https://www.youtube.com/watch?v=2WpBVanEn3M&list=PLuyTk2_mYISIZICCCdK7sLjKN1s1z9OQi&index=2

Difficulty: Apprentice \
Lab URL: https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/authentication-apprentice/authentication/multi-factor/lab-2fa-simple-bypass \
Vulnerability:  \
Tools:  \
Status:

## Lab Description
This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, access Carlos's account page.

- Your credentials: `wiener:peter`
- Victim's credentials `carlos:montoya`

## Discovery and Exploitation
1. I opened the web application and logged in as user: `wiener` using the credentials provided.

After entering the credentials, I was redirected to another page and asked to enter the 4-digit security code which I retrieve from the email client.

I clicked `Email client` to open email and retrieve the 4-digit one time password (OTP).

Then I pasted in the code and clicked `Log in`.

During a test, authentication as 'carlos' with the correct password led to a 2FA prompt, but the code was inaccessible. By directly navigating to the expected post-login URL (/my-account) after initial password verification, the 2FA check was successfully bypassed. This indicates that the system's session is prematurely established upon first-factor authentication, allowing direct access to protected resources despite pending 2FA.


There is a vulnerability in the application where it does not enforce 2FA authentication so a user doesn't 

technically speaking if the attacker gets hold of the users' credentials, they could essentially gain unauthorized access to the user's account where they could access information and functionality provisioned specifically for that account.
## Root Cause and Impact

## Recommended Remediation

## Key Takeaway

Log out of wiener
Go to Burp Suite > Set intercept on
Enter Carlos's credentials > click on
Request is sent to Burp > Click "Forward"
When it makes a request to the 2FA authentication, click "Drop" to drop the request and verified if I can access carlo's account by updating the browser URL from /login to /my-account
I was able to access Carlo's account which means there is a vulnerability within the application doesn't enforce the 2FA endpoint. The system's session is prematurely established upon first-factor authentication, allowing direct access to protected resources despite pending 2FA.



