# 🖥️ MD-102 Endpoint Administrator Lab
### Enterprise-Grade Windows Deployment & Endpoint Management · Powered by Microsoft Intune, Autopilot & Entra ID

> **Certification Target:** Microsoft MD-102 — Endpoint Administrator Associate  
> **Lab Status:** 🟢 Active & Continuously Expanding  
> **Author:** Kory Borromeo | [linkedin.com/in/koryborromeo] |

---

## 📋 Project Overview

This repository documents a fully functional, hands-on homelab environment built to master and demonstrate the skills required for the **Microsoft MD-102: Endpoint Administrator Associate** certification. The lab simulates a realistic enterprise environment using **Microsoft Intune**, **Windows Autopilot**, **Entra ID (Azure AD)**, and **PowerShell automation** to manage the full lifecycle of Windows 11 endpoints — from zero-touch provisioning to compliance enforcement and security hardening.

Every configuration, policy, and deployment artifact in this repository reflects real-world best practices used by enterprise endpoint engineers. This is not a theoretical walkthrough — every step has been executed, tested, and validated in a live lab environment.

---

## 🗺️ Architecture Overview

![Architecture Diagram](images/architecture-overview.png)

> 📸 **[INSERT DIAGRAM: High-level architecture showing the relationship between Azure Tenant → Entra ID → Intune MDM Authority → Autopilot-enrolled devices → Conditional Access → App/Policy targeting groups. Use draw.io or Lucidchart. Export as PNG to `/images/architecture-overview.png`.]**

**The architecture diagram should visually capture:**
- The **Azure / Microsoft 365 tenant** as the identity and policy authority
- **Entra ID** (Azure AD) user/group structure and licensing assignments
- **Intune** as the MDM/MAM plane, with arrows to device categories
- **Windows Autopilot** deployment profile flow (OEM → Hash Upload → OOBE → Enrolled)
- **Conditional Access** policy enforcement between users, devices, and cloud apps
- **Security Baselines** and **Configuration Profiles** targeting device groups
- Lab hardware or virtual machines representing managed endpoints

---

## 🧰 Core Technologies & Skills Demonstrated

| Technology Layer | Tool / Service | Skill Demonstrated |
|---|---|---|
| **Identity & Directory** | Microsoft Entra ID (Azure AD) | User provisioning, Group-based targeting, RBAC role assignments |
| **Device Management (MDM)** | Microsoft Intune | Policy deployment, device enrollment, compliance enforcement |
| **Zero-Touch Provisioning** | Windows Autopilot | Self-deploying & user-driven Autopilot profile configuration |
| **Operating System** | Windows 11 Enterprise (22H2 / 23H2) | OS deployment, feature management, update rings |
| **Security Hardening** | Microsoft Security Baselines | CIS/STIG-aligned endpoint hardening via Intune profiles |
| **Patch Management** | Windows Update for Business (WUfB) | Update rings, deferral policies, compliance reporting |
| **Application Delivery** | Intune Win32 App / MSIX / LOB | App packaging, deployment groups, detection rules |
| **Endpoint Security** | Microsoft Defender for Endpoint (MDE) | AV policies, EDR onboarding, threat & vulnerability mgmt |
| **Conditional Access** | Entra ID Conditional Access | MFA enforcement, compliant device requirements, named locations |
| **Automation & Scripting** | PowerShell + Microsoft Graph API | Automated provisioning, bulk operations, Graph-based reporting |
| **Infrastructure as Code** | Bicep / ARM Templates | Azure resource deployment (AAD groups, Intune policy export) |
| **CI/CD** | GitHub Actions | Automated policy-as-code validation and Graph API deployment |
| **Monitoring & Analytics** | Endpoint Analytics / Log Analytics | Performance scoring, startup performance, proactive remediations |
| **Co-Management** | Intune + Configuration Manager (Optional) | Hybrid workload management, co-management authority switching |

---

## 🏗️ Key Architectural Highlights

- **🔐 Zero-Touch, Identity-First Provisioning** — Endpoints are deployed via **Windows Autopilot** in Self-Deploying and User-Driven modes. Device hash registration, Autopilot profile assignment, and ESP (Enrollment Status Page) are fully configured so a device goes from factory reset to fully managed with zero IT hands-on touch.

- **🛡️ Defense-in-Depth Security Posture** — Security is layered: **Entra ID Conditional Access** blocks non-compliant or unmanaged devices from accessing M365 resources; **Microsoft Security Baselines** enforce hardened OS settings; **Defender for Endpoint** provides real-time EDR coverage; and **compliance policies** mark devices non-compliant within minutes of a drift event.

- **📦 Automated Application Lifecycle Management** — Win32 apps are packaged using the **Microsoft Win32 Content Prep Tool**, uploaded to Intune with custom detection scripts, and scoped to dynamic Entra ID groups. Required vs. Available assignments are used strategically to model real enterprise app governance.

- **⚙️ Policy-as-Code with Graph API + GitHub Actions** — Intune Configuration Profiles and Compliance Policies are exported as JSON via the **Microsoft Graph API** and version-controlled in this repository. A **GitHub Actions** workflow validates policy JSON and can push changes back to the tenant, demonstrating GitOps principles for endpoint management.

- **📊 Proactive Remediation & Endpoint Analytics** — Custom **Proactive Remediation** scripts detect and self-heal configuration drift (e.g., misconfigured proxy settings, stale DNS entries). **Endpoint Analytics** dashboards track startup performance scores and provide benchmarking data.

---

## 📁 Repository Structure

```
md-102-intune-lab/
│
├── 📂 autopilot/
│   ├── deployment-profiles/          # Autopilot profile JSON exports
│   ├── enrollment-status-page/       # ESP configuration exports
│   └── device-hash-upload/           # Scripts for hardware hash extraction
│
├── 📂 intune-policies/
│   ├── compliance-policies/          # Platform compliance policy JSON
│   ├── configuration-profiles/       # Device config profile JSON (OMA-URI, templates)
│   ├── security-baselines/           # MDM Security Baseline exports
│   └── update-rings/                 # Windows Update for Business ring configs
│
├── 📂 app-deployment/
│   ├── win32-apps/                   # IntuneWinAppUtil packaged apps + detection scripts
│   ├── msix-packages/                # MSIX-packaged app manifests
│   └── required-apps/               # Required app assignment scoping
│
├── 📂 powershell/
│   ├── graph-api/                    # Graph API scripts (device queries, bulk actions)
│   ├── proactive-remediations/       # Detection + remediation script pairs
│   └── reporting/                    # Compliance & inventory reporting scripts
│
├── 📂 conditional-access/
│   └── policies/                     # CA policy JSON exports via Graph API
│
├── 📂 bicep/
│   └── entra-groups/                 # Bicep templates for Entra ID group provisioning
│
├── 📂 github-actions/
│   └── workflows/                    # CI/CD workflows for policy validation & deployment
│
├── 📂 docs/
│   ├── deployment-guide.md           # Full step-by-step deployment guide (this repo)
│   ├── phase-1-tenant-setup.md
│   ├── phase-2-autopilot.md
│   ├── phase-3-policies.md
│   ├── phase-4-apps.md
│   ├── phase-5-security.md
│   └── troubleshooting.md
│
├── 📂 images/                        # Screenshots & architecture diagrams
│
├── README.md                         # ← You are here
└── LICENSE
```

---

## 🚀 Quick-Start Navigation

| I want to... | Go to... |
|---|---|
| Understand the full architecture | [Architecture Overview](#️-architecture-overview) |
| Deploy Autopilot from scratch | [`docs/phase-2-autopilot.md`](docs/phase-2-autopilot.md) |
| Export/import Intune policies | [`powershell/graph-api/`](powershell/graph-api/) |
| Understand app packaging | [`docs/phase-4-apps.md`](docs/phase-4-apps.md) |
| Review security configuration | [`intune-policies/security-baselines/`](intune-policies/security-baselines/) |
| See the CI/CD pipeline | [`.github/workflows/`](.github/workflows/) |

---

## 📊 MD-102 Exam Domain Coverage

This lab provides hands-on coverage of the following official MD-102 exam skill domains:

| Exam Domain | Coverage | Lab Components |
|---|---|---|
| **Deploy Windows client** (25–30%) | ✅ Full | Autopilot profiles, ESP, deployment modes |
| **Manage identity & compliance** (15–20%) | ✅ Full | Entra ID, Conditional Access, compliance policies |
| **Manage, maintain & protect devices** (40–45%) | ✅ Full | Config profiles, update rings, MDE, baselines |
| **Manage apps & data** (10–15%) | ✅ Full | Win32/MSIX deployment, app protection policies |

---

## 🔧 Prerequisites

### Azure / Microsoft 365 Tenant
- Microsoft 365 **Business Premium**, **E3**, or **E5** license (or Developer tenant via [M365 Dev Program](https://developer.microsoft.com/en-us/microsoft-365/dev-program))
- **Intune Plan 1** license assigned to test users
- Global Administrator or Intune Administrator role

### Lab Hardware / VMs
| Component | Minimum Spec | Recommended |
|---|---|---|
| **Lab Endpoint(s)** | Windows 11-capable hardware or VM | 2–3 VMs in Hyper-V or VMware Workstation |
| **CPU** | 4 cores | 8+ cores for multiple simultaneous VMs |
| **RAM** | 8 GB | 16–32 GB |
| **Storage** | 60 GB free | 250 GB SSD |
| **TPM** | TPM 2.0 (required for Autopilot) | vTPM in hypervisor |
| **Network** | Internet access | Isolated VLAN with internet egress preferred |

### Tools Required
```
- PowerShell 7.x
- Microsoft Graph PowerShell SDK
  Install-Module Microsoft.Graph -Scope CurrentUser
- IntuneWin32App PowerShell module
  Install-Module IntuneWin32App -Scope CurrentUser
- Microsoft Win32 Content Prep Tool (IntuneWinAppUtil.exe)
- Azure CLI (optional, for Bicep deployments)
- Git
- Visual Studio Code + PowerShell Extension
```

---

*See [`docs/deployment-guide.md`](docs/deployment-guide.md) for the complete, phase-by-phase setup walkthrough.*

---

## 🛡️ Security Posture Summary

This lab enforces the following security controls, mirroring enterprise compliance requirements:

| Control | Implementation | Status |
|---|---|---|
| MFA Enforcement | Entra ID Conditional Access — All Users policy | ✅ Enforced |
| Compliant Device Requirement | CA policy requiring Intune-compliant device for M365 access | ✅ Enforced |
| BitLocker Encryption | Endpoint Protection profile — Silent enablement + Entra ID key escrow | ✅ Enforced |
| Windows Security Baseline | MDM Security Baseline (Windows 11 22H2) applied to all devices | ✅ Applied |
| Defender Antivirus | Intune Antivirus policy — Real-time protection, PUA blocking, cloud protection | ✅ Active |
| Defender for Endpoint | MDE onboarding via Intune — EDR in block mode | ✅ Active |
| Local Admin Control | LAPS (Windows LAPS) — Managed local admin with Entra ID backup | ✅ Configured |
| Firewall Policy | Endpoint security Firewall policy — Domain, Private, Public profiles | ✅ Applied |
| App Control | AppLocker / WDAC policy — Publisher and path rules | 🔄 In Progress |

---

## 🗓️ Lab Changelog

| Version | Date | Summary |
|---|---|---|
| `v1.0` | [DATE] | Initial tenant setup, Entra ID groups, Autopilot baseline |
| `v1.1` | [DATE] | Security baseline deployment, Conditional Access policies |
| `v1.2` | [DATE] | Win32 app packaging and deployment pipeline |
| `v1.3` | [DATE] | Graph API export scripts, GitHub Actions CI workflow |
| `v2.0` | [DATE] | Proactive Remediations, Endpoint Analytics, LAPS rollout |

---

## 🔭 Future Roadmap

| Priority | Feature | Description |
|---|---|---|
| 🔴 High | **Full IaC with Bicep + Graph API** | Define all Intune policies, CA rules, and Entra groups as declarative code deployed via pipeline — true GitOps for endpoint management |
| 🟡 Medium | **Microsoft Tunnel (VPN Gateway)** | Deploy the Intune-native Microsoft Tunnel gateway for secure per-app VPN access from managed mobile endpoints |
| 🟡 Medium | **WDAC (Windows Defender Application Control)** | Implement strict application allowlist using WDAC policy in Audit → Enforced mode, replacing legacy AppLocker |
| 🟢 Low | **Intune + SCCM Co-Management Lab** | Introduce an on-premises ConfigMgr environment and configure co-management workload switching to demonstrate hybrid management expertise |
| 🟢 Low | **Endpoint Analytics Deep Dive** | Build a Power BI dashboard consuming Endpoint Analytics data via Log Analytics / Azure Monitor for executive-level reporting |

---

## 📚 References & Official Documentation

- [Microsoft MD-102 Exam Skills Outline](https://learn.microsoft.com/en-us/credentials/certifications/exams/md-102/)
- [Microsoft Intune Documentation](https://learn.microsoft.com/en-us/mem/intune/)
- [Windows Autopilot Documentation](https://learn.microsoft.com/en-us/autopilot/windows-autopilot)
- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/entra/identity/)
- [Microsoft Graph API — Intune Reference](https://learn.microsoft.com/en-us/graph/api/resources/intune-graph-overview)
- [Microsoft Security Baselines](https://learn.microsoft.com/en-us/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines)

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.  
All Microsoft product names, logos, and documentation are the property of Microsoft Corporation.

---

<div align="center">

**⭐ If this project helped your MD-102 prep or inspired your own homelab, please consider starring the repository.**

*Built with ☕, PowerShell, and an unreasonable number of Intune policy refreshes.*

</div>
