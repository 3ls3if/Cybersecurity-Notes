---
icon: piggy-bank
---

# Threat Intelligence Naming Conventions

## Naming Conventions

**What Are Naming Conventions?**

* **Definition**: A set of rules for choosing names to identify threat actors, APTs (Advanced Persistent Threats), campaigns, or operations.
* **Purpose**: Helps in organizing and cataloging threat patterns, making it easier to track and analyze them.

\
**Why Different Names for the Same Threat Actor?**

*   **Human Reasons**:

    * **Operation Name Used as Threat Actor Name**: Sometimes, the name of an operation is mistakenly used as the name of the threat actor.
    * **Malware Name Used as Threat Actor Name**: Similarly, malware names can be confused with threat actor names.
    * **Vendor Miscommunication**: Different vendors might misinterpret each other's research.
    * **Journalistic Errors**: Journalists may not always correct wrong mappings in public articles.


*   **Technical Reasons**:

    * **Partial Visibility**: Vendors see different parts of the full picture (e.g., different TTPs, IOC clusters).
    * **Group Dynamics**: Threat actors might join forces or split up, sharing tools and infrastructure.


* **Operational Reasons**:
  * **Vendor Independence**: Vendors prefer to maintain their own naming conventions for flexibility and reputation.
  * **Research Credibility**: Using another vendor's name might imply that their research is more complete.

\
**Examples of Naming Conventions**

* **FireEye/Mandiant, Cisco Talos**: Use numbers like APT28 or APT34.
* **CrowdStrike, Kaspersky, Symantec**: Use descriptive names (e.g., Panda for China, Kitten for Iran).

\
**Recommendations for Naming Conventions**

* **Avoid Numbers**: Numbers can be confusing and hard to track over time.
* **Avoid Tool-Based Names**: Naming after tools can create confusion if multiple campaigns use the same tool.
* **Be Creative and Flexible**: Adding humor or unique elements can make names easier to remember.
* **Base Names on Incidents**: Create names based on incidents you are directly facing, not just what you read about.

\
**Key Takeaways**

* **No Standardization**: There is no way to standardize all threat actor names due to various human, technical, and operational reasons.
* **Importance of Flexibility**: Being creative and flexible in naming conventions can help in better tracking and analysis.\


