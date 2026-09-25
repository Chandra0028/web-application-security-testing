# SQL Injection

## Overview

SQL Injection was identified within the application's wish list gift search functionality.

The vulnerability allowed attacker-controlled input to influence database queries.

## Testing Methodology

Testing was performed manually using Burp Suite.

The assessment first determined the number of columns returned by the underlying query. Database metadata was then enumerated to identify available tables and column names.

The identified database structure was subsequently used to demonstrate the security impact of the vulnerability.

## Exploitation Process

The testing process included:

1. Determining the number of columns in the underlying query.
2. Enumerating database tables.
3. Enumerating columns within the `users` table.
4. Identifying user-related database fields.
5. Demonstrating extraction of user data.

## Impact

Successful exploitation demonstrated the ability to:

* Enumerate the database schema
* Identify the `users` table
* Identify user-related columns
* Extract user information
* Expose password hashes

## Severity

**CVSS: 9.8 – Critical**

## OWASP Classification

**A03:2021 – Injection**

## NIST Mapping

* SI-10 – Information Input Validation
* SC-28 – Protection of Information at Rest

## Evidence

Supporting screenshots will be stored in:

```text
../evidence/sql-injection/
```

Sensitive credentials, password hashes and other access information are intentionally excluded from this repository.

## Remediation

The application should use parameterised queries or prepared statements instead of constructing SQL queries through string concatenation.

Input validation should also be implemented as a complementary security control.

## References

* OWASP Top 10
* OWASP SQL Injection Prevention Cheat Sheet
* PortSwigger Web Security Academy
