# Network Enumeration

## Objective

The initial phase of the assessment focused on identifying exposed network services and determining the attack surface of the target system.

## Tool Used

**Nmap**

The assessment used Nmap for:

* TCP port enumeration
* Service identification
* Version detection

A full TCP scan covering all 65,535 ports was performed.

## Identified Services

| Port | Service | Version       |
| ---: | ------- | ------------- |
|   21 | FTP     | vsftpd 3.0.5  |
|   22 | SSH     | OpenSSH 9.6p1 |
|   80 | HTTP    | Apache 2.4.57 |
|  139 | SMB     | Samba         |
|  445 | SMB     | Samba         |
| 3389 | RDP     | Microsoft RDP |
| 8001 | HTTP    | Apache 2.4.66 |

## Security Observations

The assessment identified multiple exposed services, increasing the overall attack surface of the target system.

Particular attention was given to:

* FTP
* SMB
* RDP
* HTTP services

Where services are not operationally required, they should be disabled. Where they must remain available, access should be restricted using appropriate firewall rules and access controls.

All retained services should also be appropriately hardened and kept up to date with security patches.

## Evidence

Screenshots and supporting evidence from the Nmap assessment will be added to the repository separately.

> **Note:** The original target IP address has been intentionally excluded from this public repository.
