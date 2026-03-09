# threat-model.md

## System Components Summary

The Smart Digitization OCR system integrates Google Cloud Vision API with HP's AI Vectorize solution to process AEC documents. Key components include:

- **HP Build Workspace Portal**: User interface for AEC professionals
- **AI Vectorize Pipeline**: Orchestration service on AWS EKS
- **OCR Service**: Text extraction coordination layer
- **Google Cloud Vision API**: External OCR processing engine
- **AWS Infrastructure**: EKS cluster, S3 storage, Secrets Manager, IAM
- **Monitoring Systems**: Splunk, Prometheus, DynamoDB for tracking and logging

## Trust Boundaries

1. **Internet → DMZ**: Untrusted internet traffic filtered through WAF and load balancer
2. **DMZ → HP Internal Network**: External users authenticated via HP OneUID/Ping MFA
3. **HP Network → AWS Private Cloud**: Internal services accessing AWS VPC with IAM controls
4. **AWS → Google Cloud**: Cross-cloud API calls using OAuth2 authentication
5. **EKS Cluster Internal**: Pod-to-pod communication within Kubernetes cluster
6. **AWS Services**: S3, Secrets Manager, and other AWS services with IAM boundaries

## STRIDE Threat Analysis Table

| Threat ID | Component | STRIDE Category | Threat Description | Risk Level | Suggested Mitigation |
|-----------|-----------|-----------------|-------------------|------------|---------------------|
| T001 | Google Cloud Vision API | Spoofing | Attacker impersonates legitimate service account | Medium | OAuth2 authentication, service account key rotation |
| T002 | OCR Service | Spoofing | Malicious service impersonates OCR endpoint | Medium | Mutual TLS, certificate validation |
| T003 | S3 Storage | Tampering | Unauthorized modification of stored documents | Medium | File integrity checks, versioning, IAM policies |
| T004 | API Communications | Tampering | Man-in-the-middle attacks on API calls | High | TLS 1.2+, certificate pinning |
| T005 | Audit Logs | Repudiation | Users deny file processing activities | Low | Comprehensive logging, digital signatures |
| T006 | Processing Pipeline | Repudiation | System actions cannot be traced | Low | Detailed audit trails, immutable logs |
| T007 | Document Content | Information Disclosure | Sensitive AEC documents exposed | High | Encryption at rest/transit, access controls |
| T008 | API Credentials | Information Disclosure | Service account keys compromised | High | Secrets Manager, key rotation, least privilege |
| T009 | Google Vision API | Denial of Service | API rate limiting or service unavailability | Medium | Rate limiting, circuit breakers, fallback mechanisms |
| T010 | EKS Cluster | Denial of Service | Resource exhaustion attacks | Medium | Resource quotas, auto-scaling, monitoring |
| T011 | AWS IAM | Elevation of Privilege | Unauthorized access to AWS resources | Medium | Least privilege, regular access reviews |
| T012 | Container Runtime | Elevation of Privilege | Container escape to host system | Medium | Security contexts, runtime protection, scanning |

## Threat Model Diagram

```mermaid
graph TB
    subgraph "Trust Boundary 1: Internet"
        Attacker[Potential Attackers]
    end
    
    subgraph "Trust Boundary 2: DMZ"
        WAF[Web Application Firewall]
        LB[Load Balancer]
    end
    
    subgraph "Trust Boundary 3: HP Internal"
        Portal[HP Build Workspace Portal]
        Auth[HP OneUID/MFA]
    end
    
    subgraph "Trust Boundary 4: AWS Private Cloud"
        subgraph "EKS Cluster"
            Pipeline[AI Vectorize Pipeline]
            OCR[OCR Service]
        end
        S3[S3 Storage]
        Secrets[Secrets Manager]
        IAM[AWS IAM]
    end
    
    subgraph "Trust Boundary 5: Google Cloud"
        Vision[Google Cloud Vision API]
    end
    
    Attacker -.->|T004: MITM Attack| WAF
    Attacker -.->|T009: DoS Attack| LB
    WAF --> LB
    LB --> Portal
    Portal --> Auth
    Auth --> Pipeline
    Pipeline -.->|T011: Privilege Escalation| IAM
    Pipeline --> OCR
    OCR -.->|T001: API Spoofing| Vision
    OCR -.->|T007: Data Exposure| Vision
    Pipeline -.->|T003: File Tampering| S3
    Pipeline -.->|T008: Credential Theft| Secrets
```

## Attack Flow Diagram

```mermaid
graph TD
    Start[Attacker Reconnaissance] --> A1{Target Selection}
    
    A1 --> B1[Attack Web Interface]
    A1 --> B2[Target API Endpoints]
    A1 --> B3[Cloud Infrastructure Attack]
    
    B1 --> C1[Credential Stuffing]
    B1 --> C2[XSS/CSRF Attacks]
    
    B2 --> D1[API Key Theft]
    B2 --> D2[Rate Limit Bypass]
    
    B3 --> E1[AWS Account Compromise]
    B3 --> E2[Container Escape]
    
    C1 --> F1[Account Takeover]
    C2 --> F2[Session Hijacking]
    
    D1 --> G1[Unauthorized API Access]
    D2 --> G2[Service Disruption]
    
    E1 --> H1[Data Exfiltration]
    E2 --> H2[Lateral Movement]
    
    F1 --> I1[Document Access]
    F2 --> I1
    G1 --> I2[OCR Service Abuse]
    G2 --> I3[System Unavailability]
    H1 --> I4[Sensitive Data Theft]
    H2 --> I5[Infrastructure Compromise]
```

## Risk Severity Table

| Risk Level | Likelihood | Impact | Threats | Priority |
|------------|------------|--------|---------|----------|
| **Critical** | High | High | - | Immediate |
| **High** | Medium | High | T004: API Tampering, T007: Data Disclosure, T008: Credential Exposure | 1-7 days |
| **Medium** | Low-Medium | Medium-High | T001: API Spoofing, T002: Service Spoofing, T003: File Tampering, T009: DoS, T011: Privilege Escalation, T012: Container Escape | 15-30 days |
| **Low** | Low | Low-Medium | T005: Activity Repudiation, T006: Action Traceability, T010: Resource Exhaustion | 30-60 days |
