# Insecure Direct Object Reference (IDOR)

## Overview

An Insecure Direct Object Reference (IDOR) vulnerability was identified in the application's message functionality.

The vulnerability allowed access to messages belonging to other users by modifying an object identifier in the request without the application performing an appropriate authorisation check.

## Location

`messages.php`

## Parameter

`id`

## Testing Methodology

The application was tested by modifying the `id` parameter associated with the requested message resource.

Different object identifiers were supplied to determine whether the application verified that the authenticated user was authorised to access the requested resource.

The assessment demonstrated that the server did not adequately validate ownership or authorisation before returning the requested message.

## Exploitation

The vulnerability could be demonstrated by:

1. Accessing a message through the application's normal functionality.
2. Identifying the object identifier used in the request.
3. Modifying the `id` parameter.
4. Submitting the modified request.
5. Observing that a message belonging to another user could be accessed.

No valid authorisation relationship was enforced between the requesting user and the referenced object.

Sensitive user data and original lab identifiers are intentionally excluded from this repository.

## Impact

Successful exploitation could allow an attacker to:

- Access other users' messages
- Bypass intended object-level access controls
- Read information belonging to other accounts
- Potentially expose sensitive user information

The impact depends on the sensitivity of the information stored within the affected messages.

## Severity

**High**

## OWASP Classification

**A01:2021 – Broken Access Control**

## NIST Mapping

- **AC-3** – Access Enforcement
- **AC-4** – Information Flow Enforcement

## Root Cause

The application relied on the object identifier supplied by the client without performing sufficient server-side authorisation checks.

Object-level authorisation should be enforced on every request rather than assuming that a user is authorised to access an object simply because they know or can modify its identifier.

## Remediation

### 1. Implement Server-Side Authorisation

The server should verify that the authenticated user has permission to access the requested object before returning its contents.

### 2. Enforce Object Ownership

Database queries should restrict returned records to objects owned by, or explicitly shared with, the authenticated user.

For example, application logic should conceptually enforce:

    Requested Object ID
            +
    Authenticated User
            ↓
    Authorisation Check
            ↓
    Return Object Only If Authorised

### 3. Do Not Rely on Client-Side Controls

Changing an identifier in a request should never provide access to another user's resources.

Security controls must be enforced on the server.

### 4. Test Access Control

The application should be tested using multiple user accounts to verify that users cannot access resources belonging to other accounts.

## Evidence

Supporting screenshots and evidence will be stored separately in:

```text
../evidence/idor/


Note: Original user identifiers, message contents and other sensitive lab information are intentionally excluded from this public repository.

References
OWASP Top 10 – Broken Access Control
OWASP Insecure Direct Object Reference Prevention
