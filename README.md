BOLA JWT API Security Lab
Project Overview

This project is a controlled cybersecurity lab focused on Broken Object Level Authorisation (BOLA) and JWT-based API security.

I built a deliberately vulnerable API using Python and Flask to understand how weak object-level authorisation can expose protected user data. The lab was tested in an isolated virtual environment using Ubuntu, Kali Linux, VMware and Burp Suite.

The purpose of this project is educational and defensive. It demonstrates why authentication alone is not enough and why APIs must also verify whether an authenticated user is authorised to access a specific object or resource.

Key Skills Practised
API security analysis
JWT authentication concepts
Broken Object Level Authorisation assessment
Request and response analysis
Burp Suite traffic inspection
Python Flask API development
Secure development awareness
Server-side authorisation checks
Security findings documentation
Mitigation planning
Tools and Technologies
Python
Flask
JSON Web Token (JWT)
Ubuntu
Kali Linux
VMware
Burp Suite
Git and GitHub
Lab Environment

The lab used two virtual machines in an isolated network:

Machine	Purpose
Ubuntu	Hosted the vulnerable Flask API
Kali Linux	Used as the security assessment environment

The Flask API was configured to run locally in the lab environment and included:

A login endpoint for authentication
JWT token generation after successful login
A protected user data endpoint
An intentionally missing object-level authorisation check
Security Issue Demonstrated

The main vulnerability demonstrated in this project was Broken Object Level Authorisation (BOLA).

BOLA occurs when an API checks that a user is authenticated but does not properly check whether that user is authorised to access the requested object.

In this lab, the API accepted user-controlled object identifiers without properly verifying ownership on the server side. This showed how an authenticated user could potentially access data that should belong to another user if object-level authorisation checks are missing.

Why This Matters

Authentication and authorisation are different security controls.

A valid JWT can prove that a user is logged in, but it does not automatically mean the user should be allowed to access every resource. The API must still check whether the authenticated user owns or has permission to access the requested data.

This project helped me understand how weak API design can create serious security risks even when login and token-based authentication are working.

Testing Approach

The API was analysed in a controlled lab environment using Burp Suite.

The assessment focused on:

Reviewing login requests
Inspecting JWT-based authentication
Analysing protected API requests
Identifying missing authorisation checks
Understanding how object identifiers can be misused
Reviewing defensive mitigation strategies

No real systems, real user data or third-party services were targeted.

Mitigation Summary

The main fix is to enforce server-side object-level authorisation on every protected endpoint.

Recommended mitigations include:

Verify authorisation on every protected request
Extract the authenticated user ID from the JWT
Compare the JWT user ID with the requested resource owner
Avoid trusting user-controlled object IDs
Apply least-privilege access principles
Use role-based access control where suitable
Log suspicious access patterns
Review code for insecure direct object reference issues
Carry out regular security assessments and code reviews
Example Authorisation Logic

The vulnerable behaviour happens when the API checks only whether a JWT is valid, but does not check whether the requested object belongs to the authenticated user.

A safer approach is:

if authenticated_user_id != requested_resource_owner_id:
    return {"error": "Access denied"}, 403

This ensures that a user can only access data they are authorised to view.

Screenshots

Screenshots can be added to the screenshots/ folder.

Suggested screenshots:

Screenshot	Description
flask-api-running.png	Flask API running in the Ubuntu lab environment
login-request-jwt-redacted.png	Login request showing JWT authentication with token redacted
burp-request-analysis-redacted.png	Burp Suite request analysis with sensitive values removed
bola-authorisation-issue.png	Demonstration of the missing authorisation check
server-side-authorisation-fix.png	Fixed authorisation logic or mitigation example

Sensitive values such as passwords, tokens, secrets and personal information should be removed or blurred before uploading screenshots.

Suggested Repository Structure
bola-jwt-api-security-lab/
│
├── README.md
├── DISCLAIMER.md
├── requirements.txt
├── .gitignore
│
├── app/
│   ├── main.py
│   ├── auth.py
│   ├── routes.py
│   └── database.py
│
├── docs/
│   ├── lab-overview.md
│   ├── threat-analysis.md
│   ├── mitigation-notes.md
│   └── lessons-learned.md
│
├── screenshots/
│   ├── flask-api-running.png
│   ├── login-request-jwt-redacted.png
│   ├── burp-request-analysis-redacted.png
│   ├── bola-authorisation-issue.png
│   └── server-side-authorisation-fix.png
│
└── findings/
    ├── vulnerability-summary.md
    └── remediation-summary.md
What I Learned

This project strengthened my understanding of API security and access control. The most important lesson was that secure authentication is not enough on its own. APIs must also enforce authorisation checks on the server side.

Through this lab, I improved my understanding of:

How JWT authentication works
Why object-level authorisation is important
How Burp Suite can be used for defensive API analysis
How weak authorisation can expose sensitive data
How server-side checks can reduce API security risks
Disclaimer

This project was completed in a controlled lab environment for educational and defensive cybersecurity learning only.

It does not target any real system, company, user account or live service. All testing was carried out in an isolated environment using intentionally vulnerable lab components.

Do not use this project to test or access systems without permission.
