# Information Disclosure

## Overview

Several information disclosure issues were identified during the security assessment.

The application exposed technical information and sensitive paths that could assist an attacker during reconnaissance and further exploitation.

The identified issues included:

- Web server and software version disclosure
- PHP version disclosure
- Sensitive paths exposed through `robots.txt`
- Disclosure of database and user-related information through SQL Injection
- Exposure of password hashes during database enumeration

## Version Information Disclosure

The web application disclosed software and server version information through its HTTP responses.

The assessment identified Apache and PHP version information associated with the application.

Exposing detailed software versions can assist attackers in identifying potential vulnerabilities associated with specific versions of software.

### Impact

Version disclosure can help an attacker:

- Identify technologies used by the application
- Determine potential attack paths
- Search for vulnerabilities affecting specific software versions
- Improve the accuracy of targeted reconnaissance

### Severity

**Medium**

### OWASP Classification

**A05:2021 – Security Misconfiguration**

### NIST Mapping

- **CM-6** – Configuration Settings
- **SI-12** – Information Management and Retention

## Sensitive robots.txt Paths

The application's `robots.txt` file disclosed paths that provided additional information about the application's structure.

While `robots.txt` is not an access-control mechanism, exposing sensitive or administrative paths can provide useful reconnaissance information to an attacker.

### Impact

An attacker could use the disclosed paths to:

- Identify potentially sensitive application locations
- Discover additional attack surfaces
- Prioritise further testing

### Severity

**Medium**

### OWASP Classification

**A05:2021 – Security Misconfiguration**

### NIST Mapping

- **CM-6** – Configuration Settings
- **AC-3** – Access Enforcement

## Database Information Disclosure

The SQL Injection vulnerability allowed database information to be enumerated.

Testing demonstrated that an attacker could identify database structures and user-related fields.

The assessment also demonstrated exposure of password hashes.

Actual database records, usernames, email addresses and password hashes are intentionally excluded from this repository.

### Impact

Successful exploitation could expose:

- Database structure
- Table names
- Column names
- User-related information
- Password hashes

This information could subsequently be used to support further attacks.

## Credential Information Disclosure

During the controlled assessment, password-related information was recovered from the vulnerable application.

The assessment demonstrated that passwords were protected using the MD5 hashing algorithm.

The recovered credentials and original password values are intentionally excluded from this public repository.

### Security Concern

MD5 is not appropriate for securely storing user passwords.

Password storage should use a modern password hashing algorithm designed specifically for password protection, such as:

- Argon2
- bcrypt
- scrypt

Each password should also use a unique cryptographic salt.

## Remediation

### 1. Remove Unnecessary Version Information

Server and application responses should avoid exposing detailed software version information where it is not required.

### 2. Review robots.txt

Sensitive or administrative paths should not be disclosed unnecessarily through `robots.txt`.

Access to sensitive resources must be controlled through server-side authentication and authorisation.

### 3. Prevent Database Enumeration

SQL Injection vulnerabilities must be eliminated using:

- Parameterised queries
- Prepared statements
- Server-side input validation

### 4. Use Secure Password Hashing

Passwords should be stored using a password hashing algorithm designed for secure password storage.

MD5 should not be used for password storage.

### 5. Minimise Information Exposure

The application should follow the principle of least information disclosure and only expose information required for legitimate functionality.


Note: Target addresses, usernames, email addresses, password hashes, recovered passwords and other sensitive lab information are intentionally excluded from this public repository.

### References
- OWASP Top 10 – Security Misconfiguration
- OWASP Password Storage Cheat Sheet
- OWASP Information Exposure
- NIST Cybersecurity Framework

## Evidence

Supporting screenshots and evidence will be stored separately in:

```text
../evidence/information-disclosure/
