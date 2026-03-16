# Compliance Mapping Matrix

## STRIDE-Based Security Requirements Compliance Mapping

| Component | Threat ID | Security Requirement | NIST Control | OWASP Reference | MITRE ATT&CK Technique |
|-----------|-----------|---------------------|--------------|-----------------|------------------------|
| Google Cloud Vision API Authentication | T-001 | OAuth2 credentials must be securely stored in AWS Secrets Manager with 90-day rotation and comprehensive access logging | IA-5 (Authenticator Management), SC-12 (Cryptographic Key Establishment), AU-2 (Audit Events) | OWASP ASVS 2.6.2 (Credential Storage), OWASP Top 10 A07:2021 (Identification and Authentication Failures) | T1078 (Valid Accounts), T1552.001 (Credentials in Files) |
| HP Build Workspace Portal | T-002 | Multi-factor authentication SHALL be enforced for all user accounts with SAML assertion encryption and 30-minute session timeout | IA-2(1) (MFA for Network Access), IA-2(2) (MFA for Privileged Accounts), SC-23 (Session Authenticity) | OWASP ASVS 2.1.1 (Password Security), OWASP Top 10 A07:2021 (Identification and Authentication Failures) | T1078 (Valid Accounts), T1110 (Brute Force), T1556 (Modify Authentication Process) |
| File Upload Interface | T-003 | All uploaded files SHALL be validated for file type, scanned for malware, and size-limited with sandboxed processing | SI-3 (Malicious Code Protection), SI-10 (Information Input Validation), SC-39 (Process Isolation) | OWASP ASVS 12.1.1 (File Upload Verification), OWASP Top 10 A03:2021 (Injection) | T1204.002 (Malicious File), T1566.001 (Spearphishing Attachment), T1105 (Ingress Tool Transfer) |
| Data in Transit to Google Cloud Vision API | T-004 | TLS 1.3 with certificate pinning SHALL be enforced for all external API communications with request signing | SC-8 (Transmission Confidentiality), SC-8(1) (Cryptographic Protection), SC-13 (Cryptographic Protection) | OWASP ASVS 9.1.1 (Communications Security), OWASP Top 10 A02:2021 (Cryptographic Failures) | T1557 (Adversary-in-the-Middle), T1040 (Network Sniffing), T1071.001 (Web Protocols) |
| AWS S3 Storage | T-005 | S3 versioning and object lock SHALL be enabled with least privilege bucket policies and integrity checksums | SC-28 (Protection of Information at Rest), AC-3 (Access Enforcement), SI-7 (Software, Firmware, and Information Integrity) | OWASP ASVS 8.3.4 (Sensitive Data Protection), OWASP Top 10 A01:2021 (Broken Access Control) | T1565.001 (Stored Data Manipulation), T1530 (Data from Cloud Storage Object) |
| Processing Queue | T-006 | All user actions SHALL be logged with immutable timestamps, user IDs, and digital signatures for non-repudiation | AU-2 (Audit Events), AU-9 (Protection of Audit Information), AU-10 (Non-repudiation) | OWASP ASVS 7.1.1 (Log Content Requirements), OWASP Top 10 A09:2021 (Security Logging and Monitoring Failures) | T1070.001 (Clear Windows Event Logs), T1562.002 (Disable Windows Event Logging) |
| OCR Processing Logs | T-007 | Logs SHALL be sent to centralized SIEM in real-time with write-once storage and cryptographic integrity verification | AU-4 (Audit Storage Capacity), AU-6 (Audit Review, Analysis, and Reporting), AU-9(2) (Audit Backup on Separate Physical Systems) | OWASP ASVS 7.1.2 (Log Processing Requirements), OWASP Top 10 A09:2021 (Security Logging and Monitoring Failures) | T1070 (Indicator Removal on Host), T1485 (Data Destruction), T1565.001 (Stored Data Manipulation) |
| Google Cloud Vision API Responses | T-008 | PII SHALL be masked in all logs with encryption at rest and in transit, restricted access, and DLP controls | SI-12 (Information Handling and Retention), SC-28 (Protection of Information at Rest), AC-4 (Information Flow Enforcement) | OWASP ASVS 8.3.4 (Sensitive Data Protection), OWASP Top 10 A02:2021 (Cryptographic Failures) | T1005 (Data from Local System), T1213 (Data from Information Repositories) |
| AWS Secrets Manager | T-009 | IAM policies with least privilege SHALL be implemented with VPC endpoints, automatic rotation, and access monitoring | AC-6 (Least Privilege), IA-5(7) (No Embedded Unencrypted Static Authenticators), AU-2 (Audit Events) | OWASP ASVS 2.6.2 (Credential Storage), OWASP Top 10 A07:2021 (Identification and Authentication Failures) | T1552.001 (Credentials in Files), T1555 (Credentials from Password Stores), T1078.004 (Cloud Accounts) |
| S3 Bucket Configuration | T-010 | S3 Block Public Access SHALL be enabled at bucket level with encryption requirements and regular security audits | AC-3 (Access Enforcement), AC-6 (Least Privilege), SC-28 (Protection of Information at Rest) | OWASP ASVS 8.3.1 (Sensitive Data Classification), OWASP Top 10 A01:2021 (Broken Access Control) | T1530 (Data from Cloud Storage Object), T1567.002 (Exfiltration to Cloud Storage) |
| Network Communication | T-011 | TLS 1.3 SHALL be enforced for all communications with network segmentation and VPC flow logs | SC-8 (Transmission Confidentiality), SC-7 (Boundary Protection), SI-4 (Information System Monitoring) | OWASP ASVS 9.1.1 (Communications Security), OWASP Top 10 A02:2021 (Cryptographic Failures) | T1040 (Network Sniffing), T1557 (Adversary-in-the-Middle), T1071 (Application Layer Protocol) |
| Google Cloud Vision API | T-012 | Exponential backoff with circuit breaker patterns SHALL be implemented with API quota monitoring and alerting | SC-5 (Denial of Service Protection), SI-4 (Information System Monitoring), CP-2 (Contingency Plan) | OWASP ASVS 11.1.4 (Business Logic Security), OWASP Top 10 A04:2021 (Insecure Design) | T1499 (Endpoint Denial of Service), T1498 (Network Denial of Service) |
| EKS Cluster Resources | T-013 | Kubernetes resource quotas and limits SHALL be implemented with horizontal pod autoscaling and monitoring | SC-6 (Resource Availability), SI-4 (Information System Monitoring), SC-5 (Denial of Service Protection) | OWASP ASVS 11.1.4 (Business Logic Security), OWASP Kubernetes Top 10 K04 (Lack of Resource Limits) | T1496 (Resource Hijacking), T1499.004 (Application or System Exploitation) |
| File Processing Pipeline | T-014 | Processing timeouts SHALL be implemented with file complexity validation and resource limits per job | SC-5 (Denial of Service Protection), SI-10 (Information Input Validation), SC-6 (Resource Availability) | OWASP ASVS 11.1.4 (Business Logic Security), OWASP Top 10 A04:2021 (Insecure Design) | T1499.004 (Application or System Exploitation), T1204.002 (Malicious File) |
| AWS IAM Roles | T-015 | Least privilege IAM policies SHALL be implemented with MFA for privileged operations and regular policy reviews | AC-6 (Least Privilege), IA-2(1) (MFA for Network Access), AC-2 (Account Management) | OWASP ASVS 4.1.1 (Access Control Design), OWASP Top 10 A01:2021 (Broken Access Control) | T1078.004 (Cloud Accounts), T1098 (Account Manipulation), T1484 (Domain Policy Modification) |
| Kubernetes RBAC | T-016 | Pod Security Standards (restricted) SHALL be implemented with non-root containers and security context constraints | AC-6 (Least Privilege), CM-7 (Least Functionality), SC-39 (Process Isolation) | OWASP Kubernetes Top 10 K01 (Insecure Workload Configurations), OWASP ASVS 14.2.1 (Server Configuration) | T1611 (Escape to Host), T1610 (Deploy Container), T1068 (Exploitation for Privilege Escalation) |
| API Gateway/Service Mesh | T-017 | Service mesh with mutual TLS SHALL be implemented for all inter-service communication with API gateway for external access | SC-8 (Transmission Confidentiality), AC-4 (Information Flow Enforcement), SC-7 (Boundary Protection) | OWASP ASVS 9.1.2 (Server Communications Security), OWASP Top 10 A01:2021 (Broken Access Control) | T1071 (Application Layer Protocol), T1090 (Proxy), T1572 (Protocol Tunneling) |
| Third-Party Dependencies | T-018 | Automated dependency scanning SHALL be implemented in CI/CD with SBOM maintenance and regular vulnerability patching | SA-11 (Developer Security Testing), RA-5 (Vulnerability Scanning), SI-2 (Flaw Remediation) | OWASP ASVS 14.2.1 (Server Configuration), OWASP Top 10 A06:2021 (Vulnerable and Outdated Components) | T1195.001 (Supply Chain Compromise: Software Supply Chain), T1203 (Exploitation for Client Execution) |
| OAuth2 Token Management | T-019 | Short-lived access tokens (1 hour max) SHALL be implemented with token binding and IP-based reuse detection | IA-5 (Authenticator Management), SC-23 (Session Authenticity), IA-11 (Re-authentication) | OWASP ASVS 3.2.1 (Session Binding Requirements), OWASP Top 10 A07:2021 (Identification and Authentication Failures) | T1550.001 (Application Access Token), T1528 (Steal Application Access Token) |
| ML Engine Processing | T-020 | Input validation and sanitization SHALL be implemented for all ML inputs with model performance monitoring | SI-10 (Information Input Validation), SI-15 (Information Output Filtering), SI-4 (Information System Monitoring) | OWASP ASVS 5.1.1 (Input Validation Requirements), OWASP Top 10 A03:2021 (Injection) | T1565.002 (Transmitted Data Manipulation), T1565.003 (Runtime Data Manipulation) |
| Monitoring Systems (Splunk/Prometheus) | T-021 | RBAC SHALL be implemented for monitoring systems with encryption in transit and at rest | AC-3 (Access Enforcement), SC-8 (Transmission Confidentiality), SC-28 (Protection of Information at Rest) | OWASP ASVS 7.1.1 (Log Content Requirements), OWASP Top 10 A09:2021 (Security Logging and Monitoring Failures) | T1530 (Data from Cloud Storage Object), T1213 (Data from Information Repositories) |
| PDF Processing Module | T-022 | PDF validation SHALL be implemented before processing with sandboxed environment and resource limits | SI-10 (Information Input Validation), SC-39 (Process Isolation), SC-6 (Resource Availability) | OWASP ASVS 12.1.1 (File Upload Verification), OWASP Top 10 A03:2021 (Injection) | T1204.002 (Malicious File), T1499.004 (Application or System Exploitation) |
| DXF Output Generation | T-023 | Output validation and sanitization SHALL be implemented with integrity checks | SI-10 (Information Input Validation), SI-7 (Software, Firmware, and Information Integrity), SI-15 (Information Output Filtering) | OWASP ASVS 5.5.1 (Output Encoding Requirements), OWASP Top 10 A03:2021 (Injection) | T1565.002 (Transmitted Data Manipulation), T1027 (Obfuscated Files or Information) |
| Vectorization Queue | T-024 | Message signing and verification SHALL be implemented with encrypted queue messages and access controls | SC-8 (Transmission Confidentiality), SI-7 (Software, Firmware, and Information Integrity), AC-3 (Access Enforcement) | OWASP ASVS 9.1.1 (Communications Security), OWASP Top 10 A02:2021 (Cryptographic Failures) | T1565.001 (Stored Data Manipulation), T1557 (Adversary-in-the-Middle) |
| Cross-Service Communication | T-025 | Service mesh with mutual TLS SHALL be implemented with Kubernetes service accounts and workload identity | SC-8 (Transmission Confidentiality), IA-3 (Device Identification and Authentication), AC-4 (Information Flow Enforcement) | OWASP Kubernetes Top 10 K03 (Overly Permissive RBAC), OWASP ASVS 9.1.2 (Server Communications Security) | T1557 (Adversary-in-the-Middle), T1550 (Use Alternate Authentication Material) |

---

## Additional Security Control Mappings

### Identity and Access Management Controls

| Security Requirement | NIST Control | OWASP Reference | MITRE ATT&CK Technique |
|---------------------|--------------|-----------------|------------------------|
| Multi-Factor Authentication (MFA) for all user accounts | IA-2(1), IA-2(2), IA-2(12) | OWASP ASVS 2.1.1, OWASP Top 10 A07:2021 | T1078 (Valid Accounts), T1110 (Brute Force) |
| Role-Based Access Control (RBAC) with least privilege | AC-6, AC-2, AC-3 | OWASP ASVS 4.1.1, OWASP Top 10 A01:2021 | T1078 (Valid Accounts), T1098 (Account Manipulation) |
| Secure session management with 30-minute timeout | SC-23, AC-12, SC-10 | OWASP ASVS 3.2.1, OWASP Top 10 A07:2021 | T1185 (Browser Session Hijacking), T1539 (Steal Web Session Cookie) |
| Service account credential rotation every 90 days | IA-5(7), IA-5(1), SC-12 | OWASP ASVS 2.6.2, OWASP Top 10 A07:2021 | T1552.001 (Credentials in Files), T1078.004 (Cloud Accounts) |
| Privileged access with break-glass procedures and MFA | AC-6(2), IA-2(1), AU-2 | OWASP ASVS 4.1.1, OWASP Top 10 A01:2021 | T1078.004 (Cloud Accounts), T1098 (Account Manipulation) |

### Data Protection Controls

| Security Requirement | NIST Control | OWASP Reference | MITRE ATT&CK Technique |
|---------------------|--------------|-----------------|------------------------|
| TLS 1.3 encryption for all data in transit | SC-8, SC-8(1), SC-13 | OWASP ASVS 9.1.1, OWASP Top 10 A02:2021 | T1040 (Network Sniffing), T1557 (Adversary-in-the-Middle) |
| AES-256 encryption for all data at rest | SC-28, SC-28(1), SC-13 | OWASP ASVS 8.3.4, OWASP Top 10 A02:2021 | T1005 (Data from Local System), T1530 (Data from Cloud Storage) |
| AWS KMS key management with automatic rotation | SC-12, SC-12(2), SC-12(3) | OWASP ASVS 6.2.1, OWASP Top 10 A02:2021 | T1552.004 (Private Keys), T1145 (Private Keys) |
| PII data masking in logs and monitoring systems | SI-12, SC-28, AC-4 | OWASP ASVS 8.3.4, OWASP Top 10 A02:2021 | T1005 (Data from Local System), T1213 (Data from Information Repositories) |
| Data retention policies with automated deletion | SI-12, MP-6, AU-11 | OWASP ASVS 8.3.3, GDPR Article 17 | T1485 (Data Destruction), T1070.004 (File Deletion) |

### Network Security Controls

| Security Requirement | NIST Control | OWASP Reference | MITRE ATT&CK Technique |
|---------------------|--------------|-----------------|------------------------|
| Network segmentation with separate VPCs and subnets | SC-7, SC-7(5), AC-4 | OWASP ASVS 14.2.1, OWASP Top 10 A01:2021 | T1021 (Remote Services), T1090 (Proxy) |
| Security groups with least privilege (deny by default) | AC-3, SC-7(5), CM-7 | OWASP ASVS 14.2.1, OWASP Top 10 A01:2021 | T1021 (Remote Services), T1046 (Network Service Scanning) |
| VPC Flow Logs with network intrusion detection | SI-4, SI-4(5), AU-2 | OWASP ASVS 7.1.1, OWASP Top 10 A09:2021 | T1040 (Network Sniffing), T1046 (Network Service Scanning) |
| Service mesh with mutual TLS for inter-service communication | SC-8, IA-3, AC-4 | OWASP ASVS 9.1.2, OWASP Kubernetes Top 10 K03 | T1557 (Adversary-in-the-Middle), T1071 (Application Layer Protocol) |
| VPC endpoints for private AWS service access | SC-7(4), SC-7(8), AC-4 | OWASP ASVS 14.2.1, OWASP Top 10 A01:2021 | T1530 (Data from Cloud Storage), T1078.004 (Cloud Accounts) |

### Logging and Monitoring Controls

| Security Requirement | NIST Control | OWASP Reference | MITRE ATT&CK Technique |
|---------------------|--------------|-----------------|------------------------|
| Centralized logging to Splunk SIEM in real-time | AU-4, AU-6, AU-6(1) | OWASP ASVS 7.1.1, OWASP Top 10 A09:2021 | T1070 (Indicator Removal on Host), T1562.002 (Disable Logging) |
| Security event monitoring with automated alerting | SI-4, SI-4(5), IR-4 | OWASP ASVS 7.1.2, OWASP Top 10 A09:2021 | T1562.001 (Disable or Modify Tools), T1070 (Indicator Removal) |
| Immutable audit logs with cryptographic integrity | AU-9, AU-9(2), AU-10 | OWASP ASVS 7.1.1, OWASP Top 10 A09:2021 | T1070.001 (Clear Logs), T1565.001 (Stored Data Manipulation) |
| Log retention for minimum 1 year (7 years for compliance) | AU-11, SI-12, MP-6 | OWASP ASVS 7.1.1, SOX, GDPR | T1485 (Data Destruction), T1070.004 (File Deletion) |
| Comprehensive audit trails for all user and API actions | AU-2, AU-3, AU-12 | OWASP ASVS 7.1.1, OWASP Top 10 A09:2021 | T1070 (Indicator Removal on Host), T1562.002 (Disable Logging) |

### Container and Orchestration Security Controls

| Security Requirement | NIST Control | OWASP Reference | MITRE ATT&CK Technique |
|---------------------|--------------|-----------------|------------------------|
| Container image vulnerability scanning before deployment | RA-5, SA-11, SI-2 | OWASP Kubernetes Top 10 K05, OWASP Top 10 A06:2021 | T1525 (Implant Internal Image), T1610 (Deploy Container) |
| Pod Security Standards (restricted profile) enforcement | CM-7, AC-6, SC-39 | OWASP Kubernetes Top 10 K01, OWASP ASVS 14.2.1 | T1611 (Escape to Host), T1610 (Deploy Container) |
| Kubernetes resource quotas and limits per namespace | SC-6, SC-5, SI-4 | OWASP Kubernetes Top 10 K04, OWASP ASVS 11.1.4 | T1496 (Resource Hijacking), T1499.004 (Application Exploitation) |
| Kubernetes network policies with default deny | SC-7, AC-4, CM-7 | OWASP Kubernetes Top 10 K03, OWASP ASVS 14.2.1 | T1021 (Remote Services), T1071 (Application Layer Protocol) |
| Kubernetes secrets encryption at rest with External Secrets | SC-28, IA-5(7), SC-12 | OWASP Kubernetes Top 10 K02, OWASP ASVS 2.6.2 | T1552.007 (Container API), T1078.004 (Cloud Accounts) |

### Vulnerability Management Controls

| Security Requirement | NIST Control | OWASP Reference | MITRE ATT&CK Technique |
|---------------------|--------------|-----------------|------------------------|
| Weekly infrastructure vulnerability scanning | RA-5, RA-5(2), RA-5(5) | OWASP ASVS 14.2.1, OWASP Top 10 A06:2021 | T1190 (Exploit Public-Facing Application), T1203 (Exploitation for Client Execution) |
| Daily application dependency scanning | RA-5, SA-11, SI-2 | OWASP ASVS 14.2.1, OWASP Top 10 A06:2021 | T1195.001 (Supply Chain Compromise), T1203 (Exploitation for Client Execution) |
| Critical vulnerability patching within 15 days | SI-2, SI-2(2), RA-5 | OWASP ASVS 14.2.1, OWASP Top 10 A06:2021 | T1190 (Exploit Public-Facing Application), T1068 (Privilege Escalation) |
| Software Bill of Materials (SBOM) maintenance | SA-4(6), CM-8, SA-11 | OWASP ASVS 14.2.1, OWASP Top 10 A06:2021 | T1195.001 (Supply Chain Compromise), T1195.002 (Software Supply Chain) |
| Automated dependency patching in CI/CD pipeline | SI-2, SA-11, RA-5 | OWASP ASVS 14.2.1, OWASP Top 10 A06:2021 | T1195.001 (Supply Chain Compromise), T1203 (Exploitation for Client Execution) |

---

**Compliance Mapping Matrix Version:** 1.0  
**Last Updated:** 2024  
**Classification:** Internal - Security Sensitive  
**Mapping Standards:**
- NIST SP 800-53 Revision 5
- OWASP Application Security Verification Standard (ASVS) 4.0
- OWASP Top 10 2021
- OWASP Kubernetes Top 10
- MITRE ATT&CK Framework v14

**Document Owner:** Senior Cybersecurity Compliance Mapping Specialist  
**Review Cycle:** Quarterly or upon framework updates