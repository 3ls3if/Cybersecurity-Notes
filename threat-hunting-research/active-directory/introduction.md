---
icon: torii-gate
---

# Introduction

## Active Directory: Architecture and Components

**Active Directory (AD) Overview**

* **What is Active Directory?**\
  Active Directory (AD) is a service developed by Microsoft for Windows Domain networks. It acts as a central database and set of services that help organize and manage network resources like users, computers, printers, and other devices within a network.

\
**Key Components of Active Directory**

* **Active Directory Domain Services (AD DS):**\
  This is the core service that stores directory information and manages communication between users and domains. It handles user login processes, authentication, and directory searches.\

* **Schema:**\
  The schema defines all the objects and attributes that the directory service uses to store data. It ensures consistency in how information is stored and accessed across the entire directory.

\
**Hierarchical Structure of Active Directory**

* **Forest:**\
  At the top level of the AD hierarchy, a forest consists of one or more AD domains that share a common schema.\

* **Domains:**\
  Domains are logical groups of objects such as users, groups, and devices within a forest. Each domain has its own security policies and relationships with other domains.\

* **Organizational Units (OUs):**\
  OUs are containers within a domain that can hold users, groups, computers, and other OUs. They help organize resources and allow administrators to define and enforce configurations and security settings through Group Policy Objects (GPOs).\


\
**Additional Features**

* **Global Catalog:**\
  The Global Catalog is a distributed data repository that contains a searchable partial representation of every object in every domain within a forest. It enables faster search and login processes across the entire forest.\


{% hint style="success" %}
Understanding these components and their roles within Active Directory is crucial for managing and securing network resources effectively. In your field, mastering these concepts will help you proactively protect AD environments and respond to potential threats.
{% endhint %}



***

## Active Directory Services and Roles

1.  **Active Directory Domain Services (AD DS):**\


    * **Function:** Stores directory data and manages user and domain interactions, such as user log-ons and directory searches.
    * **Example:** When you log onto your computer at work, AD DS verifies your credentials and grants you access to network resources.


2. **Flexible Single Master Operations (FSMO) Roles:**\

   * **Schema Master:**
     * **Function:** Manages changes to the Active Directory schema, which defines the classes of objects and attributes.
     * **Note:** Only one domain controller in the entire forest holds this role.\

   * **Domain Naming Master:**
     * **Function:** Handles the addition and removal of domains in the forest, ensuring unique and properly registered domain names.
     * **Note:** Only one domain naming master per forest.\

   * **RID Master:**\

     * **Function:** Allocates pools of relative IDs (RIDs) to other domain controllers within a domain, essential for creating new objects.\

   *   **PDC Emulator:**

       * **Function:** Handles password changes, time synchronization, and acts as the authoritative source for group policy updates.


   * **Infrastructure Master:**
     * **Function:** Updates references from objects in its domain to objects in other domains, ensuring accurate and consistent data.\

3.  **Global Catalog:**

    * **Function:** A distributed directory that enables fast object searches and log-on processes across the entire forest by containing a partial replica of all objects in the directory.

    \


{% hint style="success" %}
These roles and services are crucial for maintaining the integrity, efficiency, and security of Active Directory. Understanding them will help you manage and protect your network resources more effectively.
{% endhint %}



***

## Active Directory Security Model

1. **Authentication:**
   * **Purpose:** Verifies the identity of users and computers.
   * **Process:** When you log onto the network, Active Directory checks your credentials (username and password) to confirm your identity.
   * **Protocol Used:** Kerberos, a secure and efficient network authentication protocol developed at MIT. It uses a ticket-based system where a trusted third party (Key Distribution Center) issues time-limited tickets to prove identities.\

2. **Authorization:**
   * **Purpose:** Determines what authenticated users are allowed to do.
   * **Process:** Assigns permissions to user accounts or groups, specifying who can access specific resources and what actions they can perform.
   * **Tools:** Access Control Lists (ACLs) attached to objects like files, folders, and user accounts.\

3.  **Security Principles:**

    * **Components:** Users, groups, and computer accounts that can be assigned permissions.
    * **Management:** Effective management of these principles is crucial for maintaining a secure environment. Group-based access control simplifies management by allowing administrators to assign permissions to groups rather than individual users.


4. **Group Policy Objects (GPOs):**
   * **Purpose:** Enforce policies across users and computers within an AD environment.
   * **Function:** Manage security settings, configurations, and access controls that affect how roles operate within the network.\

5.  **Role-Based Access Control (RBAC):**

    * **Purpose:** Regulates access to resources based on the roles of individual users within an organization.
    * **Process:** Often involves assigning users to groups with specific permissions, ensuring the principle of least privilege.

    \


{% hint style="success" %}
Understanding these concepts will help you protect sensitive information and maintain the integrity of your network.
{% endhint %}



