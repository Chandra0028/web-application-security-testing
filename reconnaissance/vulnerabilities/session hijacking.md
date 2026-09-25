# Session Hijacking

## Overview

A session hijacking vulnerability was demonstrated during the authorised security testing of the web application.

The issue was identified as a consequence of the application's client-side session security configuration and the presence of Cross-Site Scripting vulnerabilities.

The assessment demonstrated that session information accessible to client-side JavaScript could be exposed and subsequently used to access an authenticated session.

## Attack Chain

The session hijacking demonstration involved the following sequence:

1. Identify a Cross-Site Scripting vulnerability.
2. Execute JavaScript within the authenticated user's browser context.
3. Demonstrate access to session information available to client-side scripts.
4. Capture the session identifier in the controlled lab environment.
5. Test the captured session in a separate browser session.
6. Confirm that the authenticated session could be accessed without entering the user's password.

The demonstration was performed only within the authorised university security testing laboratory.

## Root Cause

The attack was enabled by a combination of:

- Cross-Site Scripting vulnerabilities
- Session information being accessible to client-side JavaScript
- Insufficient protection of authentication session data

The XSS vulnerabilities provided the execution context, while the session configuration increased the potential impact of the attack.

## Impact

Successful session hijacking could allow an attacker to:

- Access an authenticated user's account
- Bypass normal password authentication
- Perform actions using the victim's authenticated session
- Potentially access information available to the compromised account

The severity of the impact depends on the privileges and sensitive information associated with the compromised account.

## Severity

**High**

## OWASP Classification

**A07:2021 – Identification and Authentication Failures**

The session security issue is associated with weaknesses in authentication and session management.

The underlying XSS vulnerabilities are separately classified under:

**A03:2021 – Injection**

## NIST Mapping

- **IA-5** – Authenticator Management
- **SC-23** – Session Authenticity

## Remediation

### 1. Protect Session Cookies

Authentication cookies should use appropriate security attributes, including:

- `HttpOnly`
- `Secure`
- Appropriate `SameSite` settings

The `HttpOnly` attribute helps prevent client-side JavaScript from directly accessing the session cookie.

### 2. Prevent Cross-Site Scripting

The application should address the underlying XSS vulnerabilities through:

- Context-aware output encoding
- Server-side input validation
- Appropriate sanitisation
- Content Security Policy (CSP)

### 3. Regenerate Sessions After Authentication

Session identifiers should be regenerated after authentication and other security-sensitive events to reduce the risk of session fixation and session reuse.

### 4. Implement Session Expiration

Sessions should have appropriate:

- Idle timeouts
- Absolute timeouts
- Server-side invalidation mechanisms

### 5. Invalidate Compromised Sessions

The application should provide mechanisms to invalidate active sessions when compromise is suspected or when a user logs out.

## Evidence

Supporting screenshots and evidence will be stored separately in:

```text
../evidence/xss/

Note: Actual session identifiers, cookies, authentication data and other sensitive lab information are intentionally excluded from this public repository.

References
OWASP Top 10 – Identification and Authentication Failures
OWASP Session Management Cheat Sheet
OWASP Cross-Site Scripting Prevention Cheat Sheet
PortSwigger Web Security Academy
