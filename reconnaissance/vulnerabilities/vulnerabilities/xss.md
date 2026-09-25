# Cross-Site Scripting (XSS)

## Overview

Two Cross-Site Scripting (XSS) vulnerabilities were identified during the assessment:

- Reflected XSS in `friends.php`
- Stored XSS in `contactus.php`

The vulnerabilities resulted from user-controlled input being rendered in the application's HTML responses without appropriate output encoding or sanitisation.

## Reflected XSS

### Location

`friends.php`

### Parameter

`img`

### Type

Reflected Cross-Site Scripting

The `img` parameter was found to reflect user-controlled input directly into the application's HTML response.

A proof-of-concept script was used during the authorised lab assessment to confirm that JavaScript supplied through the parameter could execute within the victim's browser context.

### Impact

The vulnerability demonstrated that an attacker could potentially:

- Execute JavaScript in a victim's browser
- Access information available to client-side scripts
- Manipulate page content
- Attempt to access session information where browser protections permit
- Use the vulnerability as part of a session hijacking attack

During the assessment, the vulnerability was chained with session-cookie theft to demonstrate account compromise.

## Stored XSS

### Location

`contactus.php`

### Input

Contact form message

### Type

Stored Cross-Site Scripting

The contact form was found to store attacker-controlled input on the server.

The submitted content was subsequently rendered within the application's messages section, causing the injected script to execute when the affected content was viewed.

### Impact

Because the malicious content was stored by the application, the attack could affect users who subsequently viewed the compromised content.

The assessment demonstrated that stored XSS could potentially be used to:

- Execute JavaScript in victims' browsers
- Modify displayed page content
- Create deceptive authentication prompts
- Attempt credential harvesting
- Support session compromise
- Affect multiple users who access the stored content

## Session Hijacking Demonstration

The reflected XSS vulnerability was used in the controlled lab environment to demonstrate the potential impact of session-cookie exposure.

The testing demonstrated that:

1. JavaScript executed within the victim's browser.
2. Session information accessible to client-side scripts could be exposed.
3. The captured session identifier was tested in a separate browser session.
4. The authenticated session could consequently be accessed without entering the victim's password.

This demonstrates how XSS can become significantly more damaging when combined with weak session security controls.

Sensitive session identifiers and authentication data are intentionally excluded from this repository.

## Severity

| Vulnerability | CVSS | Severity |
|---|---:|---|
| Reflected XSS | 8.2 | High |
| Stored XSS | 8.8 | High |

## OWASP Classification

**A03:2021 – Injection**

The findings are classified under the OWASP Injection category.

## NIST Mapping

- **SI-10** – Information Input Validation
- **AC-3** – Access Enforcement
- **SC-18** – Mobile Code

## Remediation

The application should implement multiple layers of protection against XSS.

### 1. Context-Aware Output Encoding

User-controlled data should be appropriately encoded before being rendered in:

- HTML
- HTML attributes
- JavaScript
- URLs

### 2. Server-Side Input Validation

Input should be validated on the server according to the expected format and context.

### 3. Sanitisation of Stored Content

User-supplied content that is stored and later displayed should be appropriately sanitised.

### 4. Content Security Policy

A strict Content Security Policy (CSP) should be implemented to reduce the ability of injected scripts to execute.

### 5. Secure Session Configuration

Session cookies should use appropriate security attributes such as:

- `HttpOnly`
- `Secure`
- Appropriate `SameSite` settings

These controls help reduce the impact of client-side attacks involving session cookies.

## Evidence

Supporting screenshots and evidence will be stored separately in:

```text
../evidence/xss/
