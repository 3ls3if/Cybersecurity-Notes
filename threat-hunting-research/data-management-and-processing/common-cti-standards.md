---
icon: standard-definition
---

# Common CTI Standards

## Common CTI Standards

1.  **Importance of Standards**:

    * Standards define how information is represented in files or communications, which is crucial for sharing and interpreting data accurately in cyber threat intelligence.


2. **Scoring Standards**:
   * **CVSS (Common Vulnerability Scoring System):**
     * Measures the severity of vulnerabilities using three metrics: base, temporal, and environmental.
     * Scores range from 0 to 10, with 10 being the most critical.
     * Example: Bluekeep (CVE-2019-0708) has a critical score of 9.8.\

3. **Threat Description or Taxonomy Standards**:
   * **OpenIOC**:
     * Introduced by Mandiant in 2011.
     * Provides a standard format for describing threat artifacts using an XML schema.\

   * **CybOX (Cyber Observable Expression)**:
     * Standardized language for representing observables, now integrated into STIX 2.0.\

   *   **STIX (Structured Threat Information Expression)**:

       * Structured language for describing cyber threat information.
       * Allows for consistent sharing, storing, and analysis of threat data.
       * Defines relationships between constructs, like linking a campaign to a threat actor.


4. **Traffic Light Protocol (TLP)**:
   * **Purpose**: TLP is a simple protocol used to label sensitive information to ensure that only the correct audience has access to it.
   * **Color Codes**:
     * **Red**: Information is highly sensitive and should only be used by you. Do not share it with anyone, even within your organization.
     * **Amber**: Information can be shared within your organization on a need-to-know basis and with clients or customers who need it to protect themselves.
     * **Green**: Information is not very sensitive and can be shared with partners or peers, but not via public channels like websites.
     * **White**: Information is public and can be shared freely, considering standard copyright rules.\

5. **Trusted Automated Exchange of Indicator Information (TAXII)**:
   * **Purpose**: TAXII is an application protocol for exchanging threat intelligence over HTTPS. It defines a RESTful API and requirements for TAXII clients and servers.
   * **Key Features**:
     * **Supports STIX**: TAXII is designed to support the exchange of threat intelligence represented in STIX format.
     * **Design Principles**: Minimizes operational changes needed for adoption, integrates easily with existing sharing agreements, and supports various threat-sharing models (Hub and Spoke, Peer to Peer, Source Subscriber).
     * **Examples**: Free TAXII servers like Limo and Hail TAXII are compatible with TAXII 2 and STIX 2.
