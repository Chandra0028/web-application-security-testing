# Web Application Security Assessment

## Overview

A controlled web application penetration testing assessment completed as
part of the MSc Cyber Security programme at the University of Roehampton.

The assessment focused on identifying, validating, exploiting and
documenting vulnerabilities within a deliberately vulnerable web
application hosted in an authorised academic cyber laboratory.

The project demonstrates practical experience in reconnaissance,
web application security testing, vulnerability analysis, exploitation,
impact assessment and remediation.

## Scope

Testing was performed against a deliberately vulnerable web application
within an isolated university laboratory environment.

The application was accessible only through the designated laboratory
network.

No public production systems were targeted.

## Tools Used

- Nmap
- Burp Suite Community Edition
- Kali Linux
- Web browser
- Manual security testing techniques

## Assessment Areas

### Network Enumeration

- Full TCP port scanning
- Service identification
- Version detection
- Attack surface analysis

### Web Application Security

- SQL Injection
- Cross-Site Scripting (XSS)
- Insecure Direct Object Reference (IDOR)
- Session security testing
- Information disclosure
- Security configuration analysis

### Credential Security

- Password hash extraction
- Analysis of weak password hashing
- Assessment of credential compromise risk

### Vulnerability Classification

Findings were assessed using:

- OWASP Top 10
- NIST security controls
- CVSS

## Key Findings

| Vulnerability | Severity |
|---|---|
| SQL Injection | Critical |
| Stored XSS | High |
| Reflected XSS | High |
| Session Hijacking | High |
| IDOR | High |
| Weak MD5 Password Hashing | High |
| Version Information Disclosure | Medium |
| Sensitive robots.txt Paths | Medium |

## SQL Injection

The assessment identified SQL injection within the application's
wish list search functionality.

Testing allowed database schema enumeration and extraction of
user-related database information.

The vulnerability was assessed as:

**CVSS: 9.8 – Critical**

Classification:

**OWASP A03:2021 – Injection**

## Cross-Site Scripting

Both reflected and stored XSS vulnerabilities were identified.

Testing demonstrated JavaScript execution within the application
and the security impact associated with exposed session information.

## IDOR

An IDOR vulnerability was identified within the messages functionality.

Manipulation of the relevant identifier allowed access to messages
belonging to other users without appropriate authorisation checks.

## Information Disclosure

Testing identified disclosure of server and software version
information through application responses.

The assessment also identified sensitive paths exposed through
the application's `robots.txt` file.

## Remediation

Recommended remediation included:

- Parameterised SQL queries
- Secure password hashing using modern algorithms
- Context-aware output encoding
- Content Security Policy
- Server-side authorisation checks
- Secure session management
- Restriction of unnecessary network services
- Reduction of unnecessary information disclosure

## Project Structure

```text
.
├── README.md
├── report/
├── reconnaissance/
├── vulnerabilities/
├── evidence/
│   ├── nmap/
│   ├── burp-suite/
│   ├── sql-injection/
│   ├── xss/
│   └── idor/
└── remediation/

Disclaimer:

This project was conducted within an authorised academic cybersecurity
laboratory environment.

The target application was deliberately vulnerable and was accessible
only through the designated laboratory network.

Credentials, passwords, session tokens, challenge answers and other
sensitive access information are intentionally excluded from this
repository.

The techniques documented here must only be used against systems where
explicit permission has been granted.
