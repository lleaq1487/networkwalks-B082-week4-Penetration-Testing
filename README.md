# Web Application Penetration Testing & Vulnerability Assessment

### WEEK 04 | WEB APPLICATION SECURITY ASSESSMENT

**Black-Box Penetration Testing · Web Application Security · Reconnaissance ·
Attack Surface Analysis · Authentication Testing · Input Validation ·
Controlled Exploitation · Data Exposure Analysis · Evidence Collection ·
Risk Assessment · Security Reporting**

## Assessment Overview

This project presents an **authorized black-box penetration testing and
vulnerability assessment** of the Mediroza General Hospital web application,
conducted as part of the **NetworkWalks B082 Week 04** cybersecurity
training program.

The assessment follows a structured security-testing methodology designed
to identify weaknesses in the target application's exposed attack surface,
validate vulnerabilities through controlled exploitation, determine their
security impact, and document actionable remediation recommendations.

The engagement was performed within a defined scope and authorized
laboratory environment. Testing was restricted to the designated target
and excluded social engineering, denial-of-service activity, and testing
outside the agreed scope.

## Assessment Objectives

The engagement was structured around four assessment milestones:

# M1 — Initial Access & Patient Report Retrieval

### MILESTONE 01 | WEB APPLICATION INITIAL ACCESS

**Reconnaissance · Attack Surface Enumeration · Authentication Analysis · SQL Injection · Authentication Bypass · Restricted Resource Access · Evidence Collection**

---

## Overview

Milestone 1 focused on obtaining initial access to the authorized **Mediroza General Hospital** web application and retrieving the three designated confidential patient laboratory reports from the restricted patient portal.

The assessment involved reconnaissance, attack-surface enumeration, analysis of the patient portal authentication mechanism, and controlled testing of user-supplied input. An **SQL injection vulnerability** was identified in the authentication functionality and successfully validated, resulting in authentication bypass and access to the restricted patient portal.

Following successful access, three encrypted patient laboratory reports were identified and retrieved for subsequent analysis in **M2 — Data Extraction**.

---

## Objectives

The objectives of M1 were to:

- Conduct reconnaissance against the authorized target.
- Identify exposed application entry points.
- Analyse the patient portal authentication mechanism.
- Analyse user-controlled input.
- Identify authentication and input-handling weaknesses.
- Validate the identified vulnerability through controlled exploitation.
- Demonstrate authentication bypass.
- Obtain access to the restricted patient portal.
- Identify the designated patient laboratory reports.
- Retrieve all three reports.
- Collect and document supporting evidence.

---

## Scope

| Parameter | Details |
|------------|---------------------------------|
| **Target** | :  https://medirozahospital.com |
| **Assessment Type** | Black-Box Penetration Test |
| **Target** | Authorized Mediroza web application |
| **Component** | Patient Portal |
| **Authorization** | Written authorization provided |
| **Testing Scope** | Target domain only |
| **Social Engineering** | Out of Scope |
| **Denial of Service** | Out of Scope |

Testing was restricted to the authorized target and defined rules of engagement.

<img width="1325" height="623" alt="Screenshot 2026-09-06 213024" src="https://github.com/user-attachments/assets/2d79abca-bda4-4c2b-9a2c-21657fd8169a" />

<img width="1336" height="641" alt="Screenshot 2026-09-06 213037" src="https://github.com/user-attachments/assets/a40df7c1-4df5-4728-b354-c65f35a2c01b" />


---

## Methodology

**M2 — Initial Access** phase.

<img width="1327" height="707" alt="Screenshot 2026-09-06 213047" src="https://github.com/user-attachments/assets/2f0cd7c0-1fd9-4cec-ac28-f9cb5fc0b885" />


The M1 assessment followed a structured initial-access workflow:

```text
Reconnaissance
      │
      ▼
Attack Surface Enumeration
      │
      ▼
Patient Portal Discovery
      │
      ▼
Authentication Analysis
      │
      ▼
Input Analysis
      │
      ▼
Vulnerability Identification
      │
      ▼
Controlled Exploitation
      │
      ▼
Authentication Bypass
      │
      ▼
Restricted Portal Access
      │
      ▼
Patient Report Discovery
      │
      ▼
Report Retrieval
      │
      ▼
Evidence Collection

```

## Attack Surface Identification

During the reconnaissance and application-analysis phase, the **Patient
Portal authentication interface** was identified as a primary attack
surface.

The login functionality was selected for further security testing because
it represents an authentication boundary protecting access to restricted
patient resources.

### Authentication Endpoint

```http
POST /patient/login.php
```
### Tested Parameter

`username`

The login functionality was selected for further manual analysis because
authentication controls represent a critical security boundary protecting
access to restricted patient resources.

## Vulnerability Identified

### SQL Injection — Patient Portal Authentication Bypass

| Attribute | Details |
|---|---|
| **Finding ID** | F-001 |
| **Vulnerability** | SQL Injection |
| **Affected Component** | Patient Portal Login |
| **HTTP Method** | `POST` |
| **Endpoint** | `/patient/login.php` |
| **Parameter** | `username` |
| **Severity** | **Critical** |
| **Impact** | Authentication bypass and unauthorized access to restricted patient resources |

The patient portal login endpoint was found to construct SQL queries using
user-controlled input without adequate parameterization or sanitization.

Controlled testing confirmed that the supplied input could influence SQL
query processing and bypass the application's intended authentication
mechanism. :contentReference[oaicite:0]{index=0}

---

## Authentication Bypass

The identified SQL injection vulnerability was validated within the
authorized assessment environment.

A controlled test against the vulnerable authentication parameter resulted
in successful authentication bypass.

The application returned an HTTP `302` response and redirected the
authenticated session to:

```text
/patient/portal.php
```
This behaviour confirmed that the application's authentication boundary
could be bypassed and that restricted functionality was accessible without
legitimate authentication credentials. :contentReference[oaicite:0]{index=0}

### Attack Flow

```text
Unauthenticated Request
        │
        ▼
Patient Portal Login
        │
        ▼
User-Controlled Input
        │
        ▼
SQL Injection
        │
        ▼
Authentication Logic Bypassed
        │
        ▼
HTTP 302 Redirect
        │
        ▼
/patient/portal.php
        │
        ▼
Restricted Patient Portal
        │
        ▼
Patient Report Discovery
        │
        ▼
Three Reports Retrieved
```

## Restricted Resource Discovery

Following successful authentication bypass, the restricted patient portal
was accessed and three confidential encrypted laboratory reports were
identified and retrieved.

| Lab Reference | Retrieved File | Status |
|---|---|---|
| `LR-2024-1187` | `patient_report_1.pdf` | **Retrieved** |
| `LR-2024-1192` | `patient_report_2.pdf` | **Retrieved** |
| `LR-2024-1205` | `patient_report_3.pdf` | **Retrieved** |

The three reports were retained as assessment artifacts for the subsequent
**M2 — Data Extraction** phase.

<img width="1332" height="707" alt="Screenshot 2026-09-06 213057" src="https://github.com/user-attachments/assets/95bc229c-73e3-4f2e-aa53-5efd6757b008" />


> **Security Note:** Original patient reports and unredacted medical
> information should not be published in a public repository. Use
> sanitized or redacted evidence instead.
>
> ## Report Protection

The retrieved reports were protected using **Adobe Standard security with RC4 128-bit encryption**.

The encryption and password-recovery process was performed as part of
**M2 — Data Extraction**.

### Recovered Passwords

| File | Password | Status |
|---|---|---|
| `patient_report_1.pdf` | `123456` | **Recovered** |
| `patient_report_2.pdf` | `password` | **Recovered** |
| `patient_report_3.pdf` | `!@#$%^&` | **Recovered** |

> **M2 Boundary:** Password recovery and analysis of the PDF protection
> mechanism belong to M2. They are listed here only as the subsequent
> outcome of the three reports retrieved during M1.
>
# M2 — Data Extraction

## M2 — Data Extraction & PDF Encryption Recovery

### MILESTONE 02 | PROTECTED DOCUMENT ANALYSIS

**Focus:** PDF Security Analysis · Encryption Identification · Password Recovery · Document Decryption · Data Extraction · Evidence Validation

---

## Overview

Following the successful retrieval of three encrypted patient laboratory
reports during **M1 — Initial Access**, M2 focused on assessing the
effectiveness of the document-level protection applied to the retrieved
files.

The objective was to determine whether the PDF encryption could be defeated
through password recovery and whether the protected report contents could
subsequently be accessed.

---

## Objectives

- Identify the encryption mechanism used by the retrieved PDF reports.
- Assess the effectiveness of the applied document protection.
- Perform password-recovery testing against all three reports.
- Decrypt the protected PDF files.
- Confirm access to the underlying report contents.
- Preserve evidence demonstrating successful data extraction.

---

## Assessment Scope

M2 was limited to the three patient laboratory reports retrieved during M1.

| Lab Reference | File | M2 Status |
|---|---|---|
| `LR-2024-1187` | `patient_report_1.pdf` | **Assessed** |
| `LR-2024-1192` | `patient_report_2.pdf` | **Assessed** |
| `LR-2024-1205` | `patient_report_3.pdf` | **Assessed** |

No additional patient documents were required for the M2 objective.

---

## Encryption Analysis

The retrieved PDF reports were protected using **Adobe Standard security
with RC4 128-bit encryption**.

The encryption mechanism was identified before password-recovery testing was
performed.

| Attribute | Details |
|---|---|
| **Document Type** | PDF |
| **Security Scheme** | Adobe Standard Security |
| **Encryption Algorithm** | RC4 |
| **Key Length** | 128-bit |
| **Protection** | Password-based |
| **Files Assessed** | 3 |

---

## Password-Recovery Testing

Password-recovery testing was performed against all three retrieved reports.

The assessment successfully recovered the passwords protecting each file,
allowing the encrypted documents to be opened and analyzed.

### Recovery Results

| File | Password | Status |
|---|---|---|
| `patient_report_1.pdf` | `REDACTED` | **Recovered** |
| `patient_report_2.pdf` | `REDACTED` | **Recovered** |
| `patient_report_3.pdf` | `REDACTED` | **Recovered** |

> **Security Note:** The actual recovered passwords are intentionally
> redacted from this public repository. Original credentials should be
> retained only within authorized assessment evidence.

---

## Decryption

After successful password recovery, each encrypted PDF was decrypted and
its protected contents became accessible.

```text
Encrypted Patient Report
          │
          ▼
Encryption Identification
          │
          ▼
Password-Recovery Testing
          │
          ▼
Password Successfully Recovered
          │
          ▼
PDF Decryption
          │
          ▼
Protected Contents Accessible
          │
          ▼
Medical Information Recovered
```
## Extraction Results

The assessment confirmed successful decryption and access to the contents of
all three retrieved reports.

| File | Encryption Identified | Password Recovered | Decrypted | Contents Accessible |
|---|---|---|---|---|
| `patient_report_1.pdf` | **Yes** | **Yes** | **Yes** | **Yes** |
| `patient_report_2.pdf` | **Yes** | **Yes** | **Yes** | **Yes** |
| `patient_report_3.pdf` | **Yes** | **Yes** | **Yes** | **Yes** |

The recovered documents contained protected medical information, confirming
that the document-level protection could be overcome once the passwords were
recovered.

---

## Evidence of Successful Extraction

The following evidence was retained during the assessment:

- Encrypted copies of the three retrieved reports.
- Evidence of the identified PDF security mechanism.
- Password-recovery results.
- Decrypted copies used for authorized analysis.
- Evidence confirming successful access to the protected report contents.

For the public repository, sensitive patient information should be replaced
with sanitized or redacted evidence.

---

## Security Impact

The assessment demonstrated that an attacker who obtained the encrypted
reports could recover their passwords and subsequently access the protected
medical information.

The weakness therefore resulted in a significant **confidentiality impact**
to sensitive patient data.

The final penetration-testing report rated the finding as **High** severity.

---

## Root Cause

The primary issue was ineffective password protection applied to the
encrypted PDF reports.

Although encryption was enabled, the passwords protecting the documents
were sufficiently weak to be recovered during the assessment.

This reduced the practical effectiveness of the document-level security
controls.

---

## Remediation

### Immediate Actions

- Replace weak passwords protecting existing reports.
- Re-encrypt affected documents using stronger security controls.
- Rotate passwords associated with previously distributed reports.
- Review access to the affected patient documents.

### Short-Term Actions

- Establish minimum password-complexity requirements.
- Prohibit predictable and commonly used document passwords.
- Use strong, randomly generated passwords where password-based protection
  is required.
- Review document-sharing and access-control procedures.

### Long-Term Actions

- Establish a formal document-protection policy.
- Periodically assess the effectiveness of document encryption.
- Implement stronger access controls for highly sensitive medical records.
- Integrate document-security requirements into the organization's broader
  security program.

---

## M2 Result Summary

| Objective | Result |
|---|---|
| Identify PDF encryption mechanism | **Completed** |
| Determine protection method | **Completed** |
| Assess document protection | **Completed** |
| Perform password-recovery testing | **Completed** |
| Recover passwords for all three reports | **Successful** |
| Decrypt all three reports | **Successful** |
| Access protected report contents | **Successful** |
| Preserve assessment evidence | **Completed** |

---

## M2 Status

**COMPLETED**

# M3 — Critical Data Exposure

<img width="1337" height="712" alt="Screenshot 2026-09-06 213109" src="https://github.com/user-attachments/assets/d5ff3014-0443-4465-b763-02f932c2aa86" />


## M3 — Critical Data Exposure & Sensitive Database Discovery

### MILESTONE 03 | CONFIDENTIAL DATABASE EXPOSURE

**Focus:** Sensitive Resource Discovery · Directory Listing · Database Backup Exposure · Database Enumeration · Salary Exposure · Shareholder Disclosure · Evidence Collection

---

## Overview

Following the successful extraction of the protected patient reports during
**M2 — Data Extraction**, M3 focused on identifying additional sensitive
resources exposed by the target web application.

During this phase, an internally generated SQL database backup was identified
within a publicly accessible historical directory.

The exposed backup contained confidential **staff and shareholder records**,
including employee salary information and corporate ownership information.

---

## Objectives

- Identify publicly accessible sensitive resources.
- Discover exposed database backups.
- Analyze the structure and contents of the exposed backup.
- Identify employee salary information.
- Identify shareholder ownership information.
- Determine the extent of the data exposure.
- Document the security impact and remediation requirements.

---

## Exposed Database Backup

A historical SQL database backup was identified at:

```text
/old/mediroza_db_backup_2019.sql
```

The backup identified itself as an internal Mediroza General Hospital
database backup generated by the Mediroza CMS backup module.

| Attribute | Details |
|---|---|
| **File** | `mediroza_db_backup_2019.sql` |
| **Location** | `/old/` |
| **Database** | `mediroza_hr` |
| **Backup Type** | SQL Database Backup |
| **Backup Date** | `2019-08-27` |
| **Exposure** | Publicly Accessible |
| **Severity** | **Critical** |

---

## Directory Listing Exposure

The historical `/old/` directory was accessible and allowed directory
enumeration.

This configuration increased the likelihood of discovering obsolete,
sensitive, or forgotten application artifacts.

| Attribute | Details |
|---|---|
| **Finding ID** | F-004 |
| **Vulnerability** | Directory Listing |
| **Affected Resource** | `/old/` |
| **Severity** | **High** |
| **Impact** | Discovery of historical and sensitive files |

## Database Structure

The exposed backup contained multiple database tables.

Two tables were particularly relevant to the M3 objective:

```text
staff
shareholders
```
### Staff Table

The `staff` table contained fields representing:

```text
id
full_name
job_title
department
email
phone
national_id
monthly_salary_zar
date_joined
```
The presence of these fields demonstrated that the exposed database contained
both personnel information and salary data.

### Shareholders Table

The `shareholders` table contained fields representing:

```text
id
shareholder_name
share_percent
shares_held
share_class
```
This provided access to sensitive corporate ownership information.

---

## Staff Data Exposure

The database contained records for **30 employees**.

The exposed fields included:

| Data Category | Status |
|---|---|
| Employee Names | **Exposed** |
| Job Titles | **Exposed** |
| Departments | **Exposed** |
| Email Addresses | **Exposed** |
| Phone Numbers | **Exposed** |
| National IDs | **Exposed** |
| Monthly Salaries | **Exposed** |
| Joining Dates | **Exposed** |

The `monthly_salary_zar` field directly exposed employee monthly salary values.

### Salary Exposure Summary

The assessment confirmed that salary information for all identified staff
records was present in the exposed database.

For public documentation, individual employee names, salaries, national IDs,
telephone numbers, and email addresses have been intentionally omitted.

---
## Shareholder Data Exposure

The database contained **10 shareholder records**.

The exposed information included:

| Data Category | Status |
|---|---|
| Shareholder Names | **Exposed** |
| Ownership Percentage | **Exposed** |
| Shares Held | **Exposed** |
| Share Class | **Exposed** |

The exposure therefore extended beyond employee information to confidential
corporate ownership data.

---

## Sanitized Evidence

The following sanitized representation demonstrates the exposed database
structure without reproducing confidential records:

```sql
CREATE TABLE `staff` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `full_name` varchar(120) NOT NULL,
  `job_title` varchar(120) NOT NULL,
  `department` varchar(80) NOT NULL,
  `email` varchar(120) NOT NULL,
  `phone` varchar(20) NOT NULL,
  `national_id` varchar(20) NOT NULL,
  `monthly_salary_zar` int(11) NOT NULL,
  `date_joined` date NOT NULL
);
```
```sql
CREATE TABLE `shareholders` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `shareholder_name` varchar(120) NOT NULL,
  `share_percent` decimal(5,2) NOT NULL,
  `shares_held` int(11) NOT NULL,
  `share_class` varchar(20) NOT NULL
);
```
## Exposure Chain

```text
Public Web Application
        │
        ▼
   `/old/` Directory
        │
        ▼
   Directory Listing
        │
        ▼
`mediroza_db_backup_2019.sql`
        │
        ▼
   `mediroza_hr`
        │
        ├──────────────────┐
        ▼                  ▼
     `staff`         `shareholders`
        │                  │
        ▼                  ▼
 Employee Records     Ownership Data
        │
        ▼
 Salary + Personal Data
```
## Corroborating Evidence

Additional evidence was identified in the assessment artifacts.

Metadata associated with one of the previously decrypted patient reports
referenced the historical database backup and its location within the
`/old/` directory.

This provided supporting evidence that the exposed backup was associated
with the application's historical deployment artifacts.

---

## Security Impact

The exposed database backup represents a **Critical** confidentiality
failure.

Unauthorized access to the backup could expose:

- Employee salary information.
- Personally identifiable employee information.
- Employment information.
- Shareholder ownership information.
- Internal database structure.

The combination of a publicly accessible backup and directory listing
substantially increased the organization's attack surface.

## Root Cause

The exposure was primarily caused by insecure handling of historical
application artifacts.

Key contributing factors included:

- Database backups stored inside a web-accessible directory.
- Insufficient access controls on historical resources.
- Directory listing enabled on `/old/`.
- Failure to remove obsolete backup files.
- Inadequate separation between application files and sensitive backups.

---

## Remediation

### Immediate Actions

- Remove the exposed SQL backup from the web-accessible environment.
- Verify that no additional copies remain within the web root.
- Disable directory listing for `/old/` and similar directories.
- Review server access logs for access to the exposed backup.
- Assess whether any credentials or secrets contained in the backup require
  rotation.

### Short-Term Actions

- Store database backups outside the web root.
- Restrict backup access through authentication and authorization controls.
- Encrypt sensitive backups at rest.
- Implement formal backup-retention and deletion procedures.
- Search the environment for additional exposed backups or configuration
  files.

### Long-Term Actions

- Establish secure backup-management standards.
- Prevent sensitive artifacts from being deployed with production
  applications.
- Implement automated detection for publicly accessible sensitive files.
- Include backup exposure testing in regular security assessments.
- Apply secure web-server configuration baselines.

---

## M3 Result Summary

| Objective | Result |
|---|---|
| Identify sensitive resources | **Completed** |
| Discover exposed SQL backup | **Successful** |
| Confirm directory listing | **Confirmed** |
| Analyze database structure | **Completed** |
| Identify employee salary information | **Successful** |
| Identify shareholder information | **Successful** |
| Validate extent of exposure | **Completed** |
| Preserve assessment evidence | **Completed** |

---

## M3 Status

**COMPLETED**

---
## Security & Privacy Notice

The original database backup contains confidential personnel and corporate
information.

The following must **not** be published in an unredacted public repository:

- Employee names
- National identification numbers
- Phone numbers
- Email addresses
- Individual salary records
- Shareholder personal information
- Raw SQL database dumps

Only sanitized database structures, redacted screenshots, aggregate findings,
and non-sensitive evidence should be included in the public repository.

---

## Responsible Use

This assessment was performed as part of the authorized **Mediroza General
Hospital Penetration Testing Project** in a controlled educational
environment.

The techniques and findings documented in this section are intended solely
for authorized security testing, validation, and remediation.

# M4 — Penetration Testing Report

<img width="1326" height="702" alt="Screenshot 2026-09-06 213122" src="https://github.com/user-attachments/assets/33177f79-3f93-4451-8c8f-f60d2fb7b4a1" />


## M4 — Final Penetration Testing Report

### MILESTONE 04 | SECURITY ASSESSMENT & REPORTING

**Focus:** Executive Summary · Scope · Methodology · Findings · Proof of Exploitation · Risk Rating · Recommendations · Remediation

---

## Executive Summary

A black-box penetration test was conducted against the authorized
**Mediroza General Hospital** web application.

The assessment successfully completed all three technical milestones:

- **M1 — Initial Access:** Authentication bypass was achieved through SQL
  injection, allowing access to the restricted patient portal and retrieval
  of three encrypted laboratory reports.
- **M2 — Data Extraction:** Weak PDF password protection was defeated,
  allowing all three encrypted reports to be decrypted and their contents
  accessed.
- **M3 — Critical Data Exposure:** A publicly accessible historical SQL
  database backup was discovered, exposing employee salary information and
  shareholder ownership data.

The assessment identified multiple security weaknesses ranging from
**Medium** to **Critical** severity.

The overall organizational risk was assessed as:

> **CRITICAL**

The most significant issues were SQL injection resulting in authentication
bypass and exposure of a sensitive database backup through a
web-accessible directory.

---

## Assessment Overview

| Attribute | Details |
|---|---|
| **Client** | Mediroza General Hospital |
| **Target** | `https://medirozahospital.com` |
| **Assessment Type** | Black-Box Penetration Test |
| **Duration** | 3 Days |
| **Assessment Date** | September 2026 |
| **Overall Risk** | **Critical** |
| **Assessment Status** | **Completed** |

---

## Scope

The assessment was conducted against the authorized Mediroza General Hospital
web application.

### In Scope

- Target web application
- Patient portal
- Authentication mechanisms
- Restricted patient resources
- Web-accessible historical resources
- Database backup exposure
- Sensitive data exposure

### Out of Scope

The following activities were excluded from the assessment:

- Social engineering
- Denial-of-Service testing
- Testing outside the authorized target
- Unauthorized access to unrelated systems

All testing was performed within the defined assessment scope.

---

## Methodology

The assessment followed a structured penetration-testing methodology:

```text
Reconnaissance
      │
      ▼
Attack Surface Identification
      │
      ▼
Authentication Analysis
      │
      ▼
Vulnerability Identification
      │
      ▼
Exploitation
      │
      ▼
Restricted Resource Access
      │
      ▼
Data Extraction
      │
      ▼
Sensitive Data Exposure Analysis
      │
      ▼
Risk Assessment
      │
      ▼
Remediation Recommendations
```
### Tools & Techniques

The assessment utilized authorized security-testing techniques and tools,
including:

- `curl`
- Python
- `pypdf`
- John the Ripper wordlists
- Manual SQL injection testing
- Standard Linux utilities

---

## Findings Summary

| ID | Finding | Severity | Impact |
|---|---|---|---|
| **F-001** | SQL Injection — Patient Portal Authentication Bypass | **Critical** | Unauthorized access to patient reports |
| **F-002** | Weak PDF Encryption Passwords | **High** | Recovery of protected medical information |
| **F-003** | Sensitive Database Backup Exposure | **Critical** | Exposure of staff and shareholder information |
| **F-004** | Directory Listing — `/old/` | **High** | Discovery of sensitive historical resources |
| **F-005** | Sensitive PDF Metadata | **Medium** | Disclosure of internal deployment information |

## Finding F-001 — SQL Injection

### Severity

**Critical**

### Description

A SQL injection vulnerability was identified in the patient portal login
function.

The vulnerable parameter was:

```text
username
```
The affected endpoint was:

```http
POST /patient/login.php
```
The vulnerability allowed authentication controls to be bypassed and resulted
in unauthorized access to the restricted patient portal.

## Impact

Successful exploitation allowed access to restricted patient resources,
including confidential laboratory reports.

## Proof of Exploitation

The application returned an HTTP 302 redirect to:
```http
/patient/portal.php
```
This demonstrated successful authentication bypass.

## Recommendation
Use parameterized SQL queries.
Implement prepared statements.
Validate and constrain user input.
Avoid constructing SQL queries directly from user-controlled input.
Perform source-code review of authentication functionality.
Implement security testing throughout the development lifecycle.

## Finding F-002 — Weak PDF Encryption Passwords

### Severity

**High**

### Description

The three laboratory reports retrieved during M1 were protected using Adobe
Standard security with RC4 128-bit encryption.

Password-recovery testing successfully recovered the passwords protecting all
three reports.

### Impact

An attacker who obtained the encrypted reports could recover their passwords
and access the protected medical information.

### Recommendation

- Replace weak document passwords.
- Use strong randomly generated passwords.
- Re-encrypt affected documents.
- Establish document-protection requirements.
- Review access controls for sensitive medical documents.

- ## Finding F-003 — Sensitive Database Backup Exposure

### Severity

**Critical**

### Description

A historical SQL database backup was discovered within the publicly
accessible `/old/` directory:

```text
/old/mediroza_db_backup_2019.sql
```
The backup contained staff and shareholder database records.

### Impact

The exposed backup contained sensitive information including:

- Employee salary information
- Personnel information
- Employment information
- Shareholder ownership information
- Internal database structure

### Recommendation

- Remove the database backup from the web root.
- Store backups outside publicly accessible directories.
- Restrict backup access through authentication and authorization.
- Encrypt backups at rest.
- Implement backup-retention and deletion procedures.
- Search for additional exposed backups.

- ## Finding F-004 — Directory Listing

### Severity

**High**

### Description

Directory listing was enabled for the historical `/old/` directory.

This configuration facilitated discovery of obsolete and sensitive application
artifacts, including the exposed SQL database backup.

### Impact

Directory enumeration increased the likelihood of discovering sensitive files
that should not have been publicly accessible.

### Recommendation

- Disable directory listing.
- Remove obsolete application artifacts.
- Restrict access to historical resources.
- Apply secure web-server configuration baselines.

---

## Finding F-005 — Sensitive PDF Metadata

### Severity

**Medium**

### Description

Metadata associated with one of the recovered patient reports contained
information referencing the historical database backup and its location.

### Impact

The metadata disclosed internal deployment information that could assist
further reconnaissance and discovery of sensitive resources.

### Recommendation

- Remove unnecessary metadata from sensitive documents.
- Establish document sanitization procedures.
- Review metadata before distributing documents externally.
- Include metadata analysis in security assessments.

- ## Overall Risk Assessment

The overall organizational risk was assessed as:

> **CRITICAL**

The combination of authentication bypass, access to confidential medical
information, weak document protection, and publicly accessible internal
database information created a significant confidentiality risk.

---

## Priority Remediation Plan

### Critical — Immediate

1. Remediate the SQL injection vulnerability.
2. Remove the exposed database backup from the web-accessible environment.
3. Disable directory listing.
4. Review server logs for access to exposed sensitive resources.
5. Assess potentially compromised credentials and secrets.

### High — Short Term

1. Strengthen PDF password protection.
2. Re-encrypt affected sensitive documents.
3. Move backups outside the web root.
4. Implement authenticated and authorized backup access.
5. Review historical application artifacts.

### Medium — Long Term

1. Implement secure software-development practices.
2. Conduct regular source-code and application security reviews.
3. Establish document-security and metadata-sanitization procedures.
4. Implement formal backup-management policies.
5. Integrate security testing into the development lifecycle.

---

## Final Assessment Conclusion

The penetration test demonstrated that multiple security controls could be
circumvented or bypassed within the authorized target environment.

The most significant findings were:

- **Critical:** SQL injection enabling patient portal authentication bypass.
- **High:** Weak PDF password protection allowing recovery of protected
  medical information.
- **Critical:** Public exposure of a sensitive database backup containing
  staff and shareholder information.
- **High:** Directory listing exposing historical application resources.
- **Medium:** Sensitive metadata disclosure.

Immediate remediation of the **Critical** findings should be prioritized,
followed by remediation of the **High** and **Medium** findings.

---

## M4 Status

**COMPLETED**
Final Security & Privacy Notice

This report contains findings from an authorized security assessment.

Patient records, employee personal information, recovered passwords, raw SQL
backups, and other confidential evidence have been intentionally excluded or
redacted from the public repository.

Public documentation should contain only sanitized evidence necessary to
demonstrate the security findings.

Responsible Use

This assessment was performed as part of the authorized Mediroza General
Hospital Penetration Testing Project in a controlled educational
environment.

The techniques and findings documented in this repository are intended
solely for authorized security testing, validation, learning, and
remediation.


```
The M4 structure follows the assignment's required sections: **Executive Summary, Scope and Methodology, Findings and Proof of Exploitation, Risk Rating, and Recommendations and Remediation**.

The findings and severity ratings are based on the final assessment report.
```
# Penetration Testing Summary

## Executive Findings Overview

The assessment identified **five security findings** across the authorized
Mediroza General Hospital web application.

| Finding | Severity | Primary Impact | Status |
|---|---|---|---|
| SQL Injection — Authentication Bypass | **Critical** | Unauthorized patient portal access | Confirmed |
| Sensitive Database Backup Exposure | **Critical** | Staff salary and shareholder data exposure | Confirmed |
| Weak PDF Encryption Passwords | **High** | Protected medical information exposure | Confirmed |
| Directory Listing — `/old/` | **High** | Sensitive historical resource discovery | Confirmed |
| Sensitive PDF Metadata | **Medium** | Internal deployment information disclosure | Confirmed |

---

## Milestone Completion

| Milestone | Description | Status |
|---|---|---|
| **M1** | Initial Access & Patient Report Retrieval | **Completed** |
| **M2** | PDF Encryption Recovery & Data Extraction | **Completed** |
| **M3** | Critical Data Exposure | **Completed** |
| **M4** | Final Penetration Testing Report | **Completed** |

---

## Overall Assessment

**Overall Risk: CRITICAL**

The assessment demonstrated multiple weaknesses affecting authentication,
confidentiality, document protection, and sensitive data storage.

The most significant risks were:

1. **Authentication bypass through SQL injection**
2. **Exposure of a sensitive database backup**
3. **Recovery of protected patient report contents**
4. **Discovery of sensitive historical resources**
5. **Disclosure of internal deployment information through document metadata**

Immediate remediation should prioritize all **Critical** findings, followed
by the **High** and **Medium** findings.

---

## Assessment Outcome

```text
M1 — Initial Access
        │
        ▼
M2 — Data Extraction
        │
        ▼
M3 — Critical Data Exposure
        │
        ▼
M4 — Final Reporting
        │
        ▼
   ASSESSMENT COMPLETE
```
> **Final Status:** All assigned Week 4 milestones were successfully
> completed within the authorized assessment scope.
