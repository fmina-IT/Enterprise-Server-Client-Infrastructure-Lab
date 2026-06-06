# Enterprise-Server-Client-Infrastructure-Lab

## 📝 Project Summary
This enterprise lab project simulates a production-grade, multi-tier network environment. By deploying a Windows Server 2022 Domain Controller and a scalable fleet of Windows 11 Pro workstations, I demonstrated core systems administration competencies, including Active Directory management, DNS resolution, and DHCP orchestration. I further engineered an enterprise OU architecture, implemented Role-Based Access Control (RBAC) for departmental resource management, and deployed robust Group Policy (GPO) baselines to ensure a secure, scalable, and standardised endpoint ecosystem.

## 📌 Project Roadmap
*   **Phase 1: Foundation Infrastructure** — Deployment of Windows Server 2022, configuration of Active Directory Domain Services (AD DS), and implementation of core network services (DNS & DHCP).
*   **Phase 2: Connecting Endpoints** — Provisioning of Windows 11 Pro workstations and secure integration into the `LAB.local` domain.
*   **Phase 3: Centralised Management** — Implementation of GPOs for security baselines, identity-driven resource mapping, and endpoint hardening.
*   **Phase 4: Enterprise Scaling** — Architecting a multi-departmental OU hierarchy, implementing Role-Based Access Control (RBAC), and establishing automated workstation lifecycle management.

## 🚀 Technical Competencies
*   **Systems Engineering:** Windows Server 2022, Active Directory Domain Services (AD DS), DNS, and DHCP.
*   **Identity & Access:** Role-Based Access Control (RBAC), OU Hierarchy Design, and Item-Level Targeting (GPP).
*   **Fleet Management:** PowerShell automation, standardised workstation naming conventions, and lifecycle management.
*   **Network Foundations:** TCP/IP configuration, virtual network architecture, and diagnostic troubleshooting (ping, nslookup, ipconfig).
*   **Security & Policy:** Group Policy (GPO) hardening, security baselines, and enterprise endpoint administration.

## 🧰 Lab Stack & Tools

- **Virtualisation Platform:** Oracle VirtualBox
- **Network Hardware (Virtual):** VirtualBox Internal Network Adapters
- **Operating Systems:** Windows Server 2022 & Windows 11 Pro (Evaluation editions)
- **Core Infrastructure Services:** Active Directory Domain Services (AD DS), DNS, DHCP
- **Administration & Automation:** PowerShell, Command Prompt, and Remote Desktop (RDP)

## 🌐 Infrastructure Specs

| Component | Role/Function |
|---|---|
| Domain Name | `LAB.local` |
| DC01 | Windows Server 2022 (Domain Controller, Static IP, DNS, DHCP) |
| Workstation Fleet | Windows 11 Pro (Managed via GPO, Departmentally segmented) |
| Network | Isolated Internal Network (VirtualBox) |

## 🌐 Infrastructure Topology
**Architectural Overview:** The environment utilies a dual-homed configuration on the Domain Controller (DC01) to logically isolate core infrastructure services from the host network. All internal traffic and domain communication are routed through a dedicated isolated virtual switch, ensuring secure, multi-tier network segmentation.

**Note on Architecture:** To balance lab flexibility with service isolation, `DC01` is currently dual-homed. In a production-hardened environment, this would be transitioned to a single-homed Domain Controller protected 
<p align="center">
  <img src="https://i.imgur.com/vTiGmS2.png" alt="Lab Architecture Diagram" width="1000">
</p>
---

# 🏗️ Phase 1: Foundation Infrastructure
---

## 📥 Step 1 | Download Windows ISO Files

Downloaded:
✅ Windows Server 2022 Evaluation ISO
✅ Windows 11 Pro ISO

Source:
Microsoft Evaluation Center

<p align="center">
  <img width="1000" src="https://i.imgur.com/1cLOUBm.png" alt="Lab Step">
</p>

---

## 🖥️ Step 2 | Create Windows Server 2022 Virtual Machine

Created a new virtual machine in Oracle VirtualBox.

Configuration:

🛠️ Operating System:
Microsoft Windows

🛠️ Version:
Windows 2022 (64 bit)

🛠️ VM Name:
WindowsServer

<p align="center">
  <img width="1000" src="https://i.imgur.com/44xdWsr.png" alt="Lab Architecture">
</p>

---

## ⚙️ Step 3 | Configure Hardware Resources

Allocated system resources for the virtual machine.

Hardware Configuration:

💾 Memory:
4096 MB RAM

🧠 Processors:
2 CPUs

💾 Disk Sie:
50 GB

This provides enough storage for:
✅ Windows Server
✅ Active Directory

🖥️ EFI Enabled:
Optional depending on setup

This step ensured the virtual machine had enough resources to run enterprise services efficiently.

<p align="center">
  <img width="1000" src="https://i.imgur.com/Yhv5gTw.png" alt="Lab Setup Step">
</p>

---

## 🪟 Step 4 | Install Windows Server 2022

Installed:
Windows Server 2022 Standard Evaluation Desktop Experience

The installation process included:
✅ System setup
✅ Initial configuration
✅ Administrator password creation

<p align="center">
  <img width="1000" src="https://i.imgur.com/Titoc6m.png" alt="Lab Setup Step">
</p>

---

## 🖧 Step 5 | Configure Server Manager

After installation, opened Server Manager to begin configuring enterprise services.

- ✅ **Network Configuration:** Assigned a static IP to ensure network stability, verified via ipconfig command-line interface.
- ✅ **System Preparation:** Renamed server to DC01 and synchronised time settings.
- ✅ **Remote Administration:** Implemented RDP for remote desktop management, ensuring secure access via restricted firewall rules. 
This enabled remote administration, reducing the need for direct console access and simulating real world server management workflows.
- ✅ **Verified System Health**
  
<p align="center">
  <img src="https://i.imgur.com/brJAigI.png" alt="Lab Step">
</p>
<p align="center">
  <img width="1000" src="https://i.imgur.com/W3cEwRK.png" alt="Lab Step">
</p>
<p align="center">
  <img width="1000" src="https://i.imgur.com/gfIyzLe.png" alt="Lab Step">
</p>

---

## 🔐 Step 6 | Install Active Directory Domain Services & DNS

Installed:
✅ Active Directory Domain Services (AD DS)
✅ DNS (Domain Name System)


Included management tools:
✅ Group Policy Management
✅ AD DS Administrative Center
✅ PowerShell Tools

This prepares the server to become a Domain Controller.

<p align="center">
  <img src="https://i.imgur.com/dl1aeuR.png" alt="Lab Step">
</p>

---

## 🌐 Step 7 | Configure Domain Controller

Configured:
✅ New Forest
✅ Root Domain
✅ DNS Services

Transformed standalone Windows Server into a centralised Domain Controller, establishing a scalable, enterprise-grade identity and security foundation.

**Key Transformation
Domain Promotion:** Promoted the server to a Domain Controller to serve as the "central brain" of the network.

**Domain Setup:** Created a new, private network "forest" and root domain to serve as a central control point and the foundation for the entire system.

**DNS Services:** Automatically set up the "address book" service, which helps every computer in the network find and communicate with each other.

**Technical Impact:** This change turned individual computers into a single, unified network. This makes the infrastructure more efficient because users only need one password to access everything Single Sign-On (SSO), and I can update security settings or manage user accounts for the entire system from one central location.

<p align="center">
  <img src="https://i.imgur.com/4F0bTgT.png" alt="Lab Step">
</p>

---

## 🌐 Step 8 | Configure DHCP Services
**Objective:** Implement dynamic IP address management to streamline endpoint onboarding and network stability.

**Action Taken:** Installed the DHCP Server role and configured a partitioned subnet scope (192.168.56.50 – 192.168.56.200).

**Key Configuration:**
 * **Scope Options:** Configured Option 003 (Default Gateway) and Option 006 (DNS Server: 192.168.56.10) to facilitate proper client connectivity and name resolution.
 * **Authorisation:** Authorised the DHCP server in Active Directory to ensure it is a trusted provider for domain-joined clients.

**Troubleshooting & Deployment Notes:**
 * **Network Isolation:** During deployment, a conflict was identified with a rogue DHCP service originating from the host-side virtual adapter.
 * **Resolution:** To maintain environment integrity, both DC01 and WS01 were migrated to a private "Internal Network" virtual switch. Service bindings on DC01 were restricted to the Internal adapter, ensuring the server exclusively serves the lab environment.

**Technical Impact:** Automates IP assignment, prevents address conflicts, and provides a stable, isolated foundation for future domain-joined workstation integration.
<p align="center">
  <img src="https://i.imgur.com/mmgQmkm.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/JdKCpiP.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/U2VNtx4.png" alt="Lab Step">
</p>
---

## 🔑 Step 9 | Configure DSRM Password

Configured the:
Directory Services Restore Mode (DSRM) password

Purpose:
The DSRM password is used for:
✅ Active Directory recovery
✅ Domain controller maintenance
✅ Disaster recovery operations

<p align="center">
  <img src="https://i.imgur.com/2PaH1ZP.png" alt="Lab Step">
</p>


---
# 🖥️ Phase 2: Connecting Endpoints

Context: Building upon the foundation established in Phase 1, this phase focuses on provisioning Windows 11 workstation users and securing their integration into the Active Directory domain for centralised authentication.

---

## 📥 Step 1 | Directory Organisation (OUs)
* **Objective:** Establish the directory structure before onboarding assets.
* **Action Taken:** Created dedicated Organisational Units (OUs) to move away from default containers and establish a scalable hierarchy (e.g., "Accounts," "Groups," "Workstations").

<p align="center">
  <img src="https://i.imgur.com/p2LqeBn.png" alt="Lab Step">
</p>

## 📥 Step 2 | Workstation Provisioning
* **Objective:** Deploy a client environment capable of enterprise management.
* **Action Taken:** Performed a clean installation of Windows 11 Pro in VirtualBox. 
* **Rationale:** I selected the Pro edition over Home to ensure support for enterprise-grade features:

    * **Domain Join Capability:** Essential for secure integration into the LAB.local Active Directory domain.
    * **Group Policy Support:** Required for enforcing Centralised Management and security baselines.
    * **Remote Desktop (RDP):** Facilitates administrative access, allowing for remote management without physical proximity to the workstation.
    * **BitLocker:** Provides device encryption to protect sensitive data at rest.

* **System Specs:** Configured with 4GB of RAM and 2 vCPUs to ensure a responsive, production-grade end-user environment for administrative tasks and background security services.

<p align="center">
  <img width="1000" src="https://i.imgur.com/ab0Ay9j.png" alt="Lab Step">
</p>

## 🌐 Step 3 | Network & Domain Integration
* **Objective:** Connect the client to the network and authenticate it to the domain.

* **Action Taken:**

    * **DNS Configuration:** Configured the IPv4 DNS settings on the Windows 11 client to point specifically to the static IP address of the Domain Controller (DC01).
    * **Connectivity Verification:** Confirmed the client could resolve the LAB.local domain before initiating the join.
    * **Domain Join:** Executed the sysdm.cpl process, authenticated with domain administrator credentials, and successfully joined the machine to the domain.
<p align="center">
  <img src="https://i.imgur.com/v6U3qyR.png" alt="Lab Step">
</p>

<p align="center">
  <img src="https://i.imgur.com/Bcs3jzW.png" alt="Lab Step">
</p>

* **Validation:** Confirmed the machine appeared in the "Computers" container and moved it into the "Workstations" OU.

## 📥 Step 4 | Infrastructure Validation
* **Objective:** Confirm successful domain integration and centralised authentication.
* **Action Taken:** Created a temporary test user ("Jim Watkins") within the Accounts OU to verify that domain-level authentication is functioning correctly across the joined WS01 workstation.
* **Result:** Successfully logged into the Windows 11 workstation using domain credentials, confirming end-to-end connectivity between the Client and DC01.
* Note: This account is a temporary placeholder used for connectivity validation. Full User Lifecycle Management and advanced AD administration will be detailed in the upcoming "Advanced Active Directory" lab.

<p align="center">
  <img src="https://i.imgur.com/oKVd65h.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/tn6tcmi.png" alt="Lab Step">
</p>

---
# 🛡️ Phase 3: Centralised Management

**Context:** With the workstations successfully joined to the LAB.local domain, this phase focuses on applying Group Policy Objects (GPOs) to enforce security baselines, standardise the user experience, and harden endpoints against unauthorised changes.

## Step 1 | Security Hardening: Endpoint Restriction
* **Objective:** Prevent unauthorised modifications to system settings to maintain a secure configuration baseline.
* **Action Taken:** Deployed a GPO titled Restrict-Workstation-Settings linked to the Workstations OU. Configured policy settings to prohibit access to the Control Panel and Windows Settings app.
* **Result:** Standard users (e.g., Jim Watkins) are prevented from altering system configurations, significantly reducing the attack surface of the endpoint.
<p align="center">
  <img src="https://i.imgur.com/5mR6pvx.png" alt="Lab Step">
</p>

## Step 2 | User Experience: Standardisation
* **Objective:** Create a consistent, professional desktop environment for all corporate users.
* **Action Taken:** Deployed a GPO titled Workstation-Environment-Policy to enforce a corporate-standard desktop wallpaper and configure specific taskbar settings.
* **Result:** All domain-joined machines now present a uniform user interface, reflecting standard enterprise branding and layout requirements.
<p align="center">
  <img src="https://i.imgur.com/atXgtgP.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/r28eShc.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/4R3xdZX.png" alt="Lab Step">
</p>

## Step 3 | Identity Security: Password Policy
* **Objective:** Enforce robust account security at the domain level.
* **Action Taken:** Created a GPO titled Domain-Password-Policy linked to the domain root. Configured settings for password complexity, minimum length, and account lockout thresholds after failed attempts.
* **Result:** Strengthened the identity foundation by ensuring all user accounts comply with enterprise-grade password security requirements.
<p align="center">
  <img src="https://i.imgur.com/RIpUTgr.png" alt="Lab Step">
</p>

## Step 4 | Data Access & Permissions: Automated Scalability

* **Objective:** Implement role-based access control (RBAC) and automated resource provisioning for departmental data.
* **Action Taken:** 
  * Created a dedicated Security Group ("HR") in Active Directory and added "Jim Watkins" as a member.
  * Configured a shared network folder ("HR") on the file server, applying NTFS permissions for "Modify" access for the "HR" group.
  * **Automation & Scalability:** Deployed a GPO (Workstation-Mapped-Drives) utilising **Group Policy Preferences (GPP)** for persistent drive mapping.
  * **Advanced Configuration:** Enabled **Loopback Processing (Replace Mode)** to ensure environment consistency across workstations and used **Security Filtering** to restrict drive mapping exclusively to the "HR" security group.
  * **Best Practice:** Utilised security groups for access control rather than individual accounts to ensure scalability, ease of auditing, and efficient user lifecycle management.
  * **Result:** Established a secure, permission-controlled file environment where users automatically receive their required resources upon login, regardless of the workstation used. This design eliminates manual per-user configuration and ensures seamless scalability for future hires.

<p align="center">
  <img src="https://i.imgur.com/HdHkZoF.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/uktRJxL.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/V0sZjj0.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/MxWxBRV.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/NNzHrbh.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/OoGvCBs.png" alt="Lab Step">
</p>

---

# 🏗️ Phase 4: Enterprise Scaling

**Context:** Transitioning from a single-user proof of concept to a multi-departmental, role-based enterprise environment.

## Step 1 | Multi-Departmental OU Hierarchy
* **Objective:** Establish a scalable directory structure to support enterprise growth.
* **Action Taken:** Architected a granular OU hierarchy under the `LAB.local` root.
    * **`_Enterprise_Assets`**: Organised into departmental sub-OUs (`HR`, `Finance`, `IT`) to allow for OU-level GPO filtering.
    * **`_Enterprise_Users`**: Mirroring the workstation structure to enable precise Delegated Administration.
* **Impact:** Provides the foundation for departmental RBAC and ensures GPO inheritance is strictly controlled.

### 🏢 Enterprise Fleet Composition
This fleet demonstrates scalable GPO distribution and departmental RBAC.
INSERT SCREENSHOT HERE
Figure 1: Enterprise OU Hierarchy. Organised by Asset and User categories with departmental sub-OUs to support GPO inheritance and granular delegation.

| Department | Users | Workstations | Asset ID Format |
| :--- | :--- | :--- | :--- |
| **HR** | 1 | 1 | HR_WS01 |
| **Finance** | 2 | 2 | FIN_WS01, FIN_WS02 |
| **IT** | 2 | 2 | IT_WS01, IT_WS02 |
<p align="center">
  <img src="https://i.imgur.com/9ZLmYHu.png" alt="Lab Verification">
</p>
*Figure 1: Enterprise OU Hierarchy showing departmental segmentation.*

## Step 2 | Scalable RBAC with Group Policy Preferences (GPP)
To maintain an enterprise-grade, clean environment, I utilised a centralised "Mapped Drives" GPO policy rather than creating departmental GPO sprawl.

* **Methodology:** I implemented **Item-Level Targeting** within a single GPO.
    * **Implementation:** Instead of static mappings, I targeted security groups (e.g., `LAB\HR`, `LAB\Finance`) to control access.
    * **Persistence:** Configured to `Replace` existing drives and **Remove the item when it is no longer applied**, ensuring users never retain access if they change departments or roles.
* **Benefits:** This approach provides a "single pane of glass" for managing enterprise-wide resource access, ensuring the infrastructure remains agile and auditable.
<p align="center">
  <img src="https://i.imgur.com/H8oyt90.png" alt="Lab Verification">
</p>
<p align="center">
  <img src="https://i.imgur.com/Ns5KNdx.png" alt="Lab Verification">
</p>
*Figure 2: GPP Item-Level Targeting interface demonstrating identity-driven resource provisioning.*

## Step 3 | Asset Management & Lifecycle
* **Objective:** Implement standardised workflows for maintaining a production-grade fleet.

#### 1. Standardised Naming & Attribution
* **Naming:** Assets follow `[Dept]_[AssetType][Number]` to eliminate collisions.
* **Accountability:** I utilised the **Managed By** attribute in AD DS to map hardware to users (e.g., `HR_WS01` managed by `Jim Watkins`).

#### 2. Administrative Renaming Workflow
Workstations remain hardened via GPO, so I utilised PowerShell for fleet management to maintain domain synchronisation.
* **Process:** `Rename-Computer` → ADUC Object Sync → `gpupdate /force`.
* **Verification:** This ensures that the workstation identity in DNS, DHCP, and AD remains consistent post-rename.

#### 3. Administrative Renaming Workflow
To maintain high-security posture, workstations remain restricted via Group Policy. Asset renaming is performed using PowerShell to bypass UI restrictions while ensuring domain synchronisation.
*   **Step 1:** Execute `Rename-Computer -NewName "NEW_NAME" -Restart` via administrative PowerShell on the target asset.
*   **Step 2:** Sync the object name in ADUC to match the new host identity.
*   **Step 3:** Perform `gpupdate /force` to confirm that GPO inheritance remains correctly applied to the renamed host.
* **Verification:** This ensures that the workstation identity in DNS, DHCP, and AD remains consistent post-rename.

<p align="center">
  <img src="https://i.imgur.com/6RxEeac.png" alt="Lab Verification">
</p>
*Figure 3: DHCP Leases confirming successful registration of the 5-workstation fleet within the defined scope.*

---

## 🛠️ Troubleshooting & Operational Resilience

This section documents key challenges encountered during the deployment and the architectural solutions implemented to ensure infrastructure reliability.

### 1. The Challenge: Session Dependency & Deployment Bloat
Initial testing revealed that manual network drive mappings were inconsistent, session-dependent, and lacked the resilience to reconnect following network stack initialisations or server restarts. Furthermore, standard GPO application lacked the granularity required to scale across multiple departments without creating "GPO bloat"—the management overhead of creating unique policies for every organisational unit.

### The Resolution: Centralised GPP with Hardened Logic
I replaced manual mapping with a centralised `Workstation-Mapped-Drives` GPO utilising **Group Policy Preferences (GPP)**. This architecture ensures persistent, secure, and identity-aware resource provisioning:

*   **Scalable Architecture (Item-Level Targeting):** Instead of individual GPOs per department, I consolidated all drive rules into a single policy. I configured each mapping entry to evaluate the user’s security group membership in real-time at login using **Item-Level Targeting**. This enforces the Principle of Least Privilege, presenting users with only the network resources authorised for their specific business function.
*   **Dynamic Persistence & Cleanup:** I set the GPO action to **"Replace,"** ensuring mappings are refreshed and strictly enforced at every policy update. Crucially, I enabled the **"Remove this item when it is no longer applied"** setting; this guarantees that if a user changes departments, their environment automatically clears unauthorised resources, maintaining a clean and secure endpoint.
*   **Operational Stability & Timing:** To guarantee a consistent user experience despite network latency, I hardened the GPO processing sequence:
    *   **Loopback Processing (Replace Mode):** Ensures workstation-specific settings override user-level conflicts, providing a predictable environment regardless of the machine used.
    *   **Network Synchronisation:** Enabled **"Always wait for the network at computer startup and logon"** to prevent "offline" logins that bypass mandatory policies.
    *   **Connectivity Buffering:** Configured a 60-second **"Workplace connectivity wait time,"** providing a reliable buffer for the network stack to reach the Domain Controller. This eliminates the intermittent "missing drive" issues caused by slow initialisation.

#### 📈 Business Impact
*   **Operational Efficiency:** Reduced IT support overhead by automating the most common "missing drive" helpdesk tickets.
*   **Productivity:** Users experience immediate access to required resources upon login, without manual intervention.
*   **Scalability & Compliance:** The centralised, identity-aware design allows for seamless future growth while ensuring strict adherence to enterprise security and audit standards.
<p align="center">
  <img src="https://i.imgur.com/KeUwOSC.png" alt="DNS Configuration Verification">
</p>
<p align="center">
  <img src="https://i.imgur.com/H8oyt90.png" alt="Lab Verification">
</p>

### 2. Group Policy Object (GPO) Scope, Inheritance, and Security Filtering
* **Structural Issue (Inheritance & OU Placement):** GPOs were initially failing due to object placement and scope.
    * **Root Cause:** Misalignment of inheritance; specifically, linking user-level policies to OUs containing only computer objects, and failing to move workstation objects from the default "Computers" container to the target "Workstations" OU.
    * **Resolution:** Re-architected the OU hierarchy and verified correct alignment of User/Computer configurations with their respective containers.
* **Permissions Issue (Security Filtering vs. Delegation):** Even after correcting the OU structure, policies remained in an "N/A" state for certain endpoints.
    * **Root Cause:** The computer accounts lacked explicit "Apply" permissions. While they had "Read" access via the **Delegation** tab, they were missing from the **Security Filtering** list. 
    * **Resolution:** Added **"Domain Computers"** to the **Security Filtering** section of the relevant GPOs to grant explicit application permissions.
    * **Outcome:** Established a hardened, predictable GPO processing pipeline where all endpoints successfully pull and apply mandatory configurations.     
<p align="center">
  <img src="https://i.imgur.com/Awj5oeN.png" alt="Lab Step">
</p>
<p align="center">
  <img src="https://i.imgur.com/5kSZ8Et.png" alt="Lab Verification">
</p>

### 3. DNS Resolution & Domain Connectivity
* **Issue**: Client workstations exhibited intermittent failures when joining the domain and resolving service records.
* **Root Cause**: 
    1. **Initial Configuration**: Clients were defaulting to ISP/router-assigned DNS servers.
    2. **Architectural Conflict**: The Domain Controller was "multi-homed," registering incorrect NAT-adapter IPs and unnecessary IPv6 records in DNS, leading to split-brain resolution.
* **Resolution**: 
    1. **Client Fix**: Updated client IPv4 settings to point exclusively to the Domain Controller (`192.168.56.10`).
    2. **DNS Hardening**: Purged stale "A" and "AAAA" records in DNS Manager and disabled IPv6 across all virtual network adapters to prevent traffic leakage.
    3. **Service Binding**: Configured the DNS Server service to bind exclusively to the **Internal Network adapter**, preventing resolution conflicts by ensuring the server ignores traffic arriving via the NAT adapter.
    4. **Verification**: Executed `nslookup lab.local` to confirm successful resolution.
* **Outcome**: Established stable, single-path name resolution, ensuring seamless domain integration and network traffic isolation.
<p align="center">
  <img src="https://i.imgur.com/4sNQtTA.png" alt="DNS Interface Binding">
</p>
<p align="center">
  <img src="https://i.imgur.com/GatdSK7.png" alt="Clean DNS Records">
</p>


---

## 🛠️ Key Skills Demonstrated

**Systems Engineering & Architectural Hardening**
* **Operational Resilience:** Established proactive infrastructure hardening and disaster recovery baselines, ensuring high availability through snapshot-based workflows and rigorous DSRM management.
* **Automated Supportability:** Optimised GPO processing and network timing parameters to ensure persistent drive mapping, effectively eliminating "missing network drive" helpdesk tickets and reducing operational support overhead.
* **Network Topology Design:** Orchestrated a secure, multi-tier virtual network using isolated Internal Network segments to eliminate host-interference and ensure traffic integrity.
* **Service-Level Hardening:** Implemented advanced interface binding for DNS and DHCP services, preventing "split-brain" resolution and ensuring service isolation in multi-homed environments.
* **DNS Infrastructure Sanitisation:** Executed systematic cleanup of stale A/AAAA records and IPv6 deprecation to maintain an authoritative and performant naming infrastructure.
* **Infrastructure Diagnostics:** Leveraged systematic root cause analysis to resolve complex GPO inheritance, domain join failures, and RPC communication issues.

**Advanced Enterprise Management & Security**
* **RBAC & Governance:** Executed least-privilege security models through granular Active Directory security groups and NTFS permission management.
* **Group Policy Orchestration (GPO/GPP):** Engineered complex policy hierarchies, utilising Group Policy Preferences (GPP), Loopback Processing, Item-Level Targeting, and Security Filtering to achieve scalable, identity-driven resource provisioning.
* **Automated Provisioning:** Designed and deployed persistent, identity-aware drive mapping workflows and fleet deployment strategies that ensure environmental consistency and high availability for domain users.
* **Attack Surface Reduction:** Applied GPOs to restrict system access (Control Panel/Settings) and enforce standardised security baselines, effectively minimising endpoint vulnerability.
* **Identity Security:** Implemented domain-wide password complexity and account lockout thresholds to mitigate brute-force and credential-based threats.

**Identity & Core Systems Administration**
* **Enterprise Architecture:** Designed and scaled a multi-OU forest/domain architecture, facilitating delegated administration and efficient asset management.
* **Active Directory Domain Services (AD DS):** Managed the full lifecycle of AD DS, from forest creation and schema organisation to multi-OU architecture design and disaster recovery.
* **Identity & Access Management:** Implemented centralised authentication (SSO) and role-based access control (RBAC) via security groups to ensure scalable and auditable resource permissions.
* **Endpoint Lifecycle Management:** Standardised Windows 11 deployment with domain-integrated security baselines, automated drive mapping, and secured RDP access for efficient remote management.
* **Virtualisation & Disaster Recovery:** Managed end-to-end virtual infrastructure, utilising snapshot-based workflows to simulate production disaster recovery and rapid environment rollbacks.

---

## 🏁 Summary of Outcomes: 
This lab successfully established an enterprise-grade Windows environment, validating core competencies in server deployment, domain integration, departmental scaling, and centralised policy management.

## 🚀 Next Steps/Future Roadmap: 
Future iterations will focus on Hybrid Identity synchronisation with Microsoft Entra ID, extending these on-premises identities to the cloud.
[Hybrid Identity Integration Lab](https://github.com/fmina-IT/Hybrid-Identity-Integration-Lab)
