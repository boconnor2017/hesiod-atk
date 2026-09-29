![header](../_atkconfig/header.png)

# Modern Private Cloud Discovery

| | |
|---|---|
| **Version** | 1.0 DRAFT |
| **Author** | Brendan O'Connor |
| **Role** | Principal Architect |
| **Reviewers** | TBD |
| **Date** | 09/29/2026 |

---

# Core Technologies

This design should incorporate all components associated with VMware Cloud Foundation 9.1.1. These components are listed in the formal release notes published by Broadcom under Bill of Materials.

# Reference Guardrails

<!-- Toolkit default domain list. The architect must confirm or replace it during
     initialization before any AI-assisted research begins. -->

This architecture is for a lab environment. All documentation sources are acceptable and will be incorporated into a functional test plan for validation later. 

# Standard Design

This design should begin with a comprehensive technical design required to deploy VMware Cloud Foundation 9.1.1 in its entirety in a non-production environment. Leverage security and hardening guide and NIST 800-53 standards for VMware as a starting point for design specifications. This design will be referred to as a Modern Private Cloud (MPC). As such the MPC incorporates the following components:

* VCF Installer/SDDC Manager 9.1.1
* ESX 9.1.1
* vCenter 9.1.1
* vSAN ESA 9.1.1
* vSAN OSA 9.1.1
* NSX 9.1.1
* VCF Operations 9.1.1
* Cloud Proxy 9.1.1
* License Server 9.1.1
* VCF Operations for Networks 9.1.1
* VCF Operations HCX 9.1.1
* VCF Automation 9.1.1 (All-Apps)
* Supervisor 9.1.1
* VMware vSphere Kubernetes Service 3.7.0+20260618
* vSphere Kubernetes Releases 1.34.2+vmware.2-vkr.2
* Fleet Lifecycle 9.1.1
* Identity Broker 9.1.1
* Log Management 9.1.1
* Real Time Metrics 9.1.1
* Real Time Metrics Store 9.1.1
* Salt RaaS 9.1.1
* Salt Master 9.1.1
* SDDC Lifecycle 9.1.1
* Software Depot 9.1.1
* Telemetry 9.1.1
* VCF Services Runtime 9.1.1
* VCF Download Tool 9.1.1
* VMware Remote Console 13.1.1
* VCF Consumption CLI 9.1.1
* VCF Consumption CLI Plugins & Databases 9.1.1
* Deep Learning VM 9.1.1
* Private AI Services 3.0.0

In addition to these components, the MPC also includes the following Supervisor Services:
* VMware vSphere Kubernetes Service 3.7.0+20260618
* Harbor 2.15.2+vmware.1-vks.1
* CA Cluster Issuer 9.1.1
* Contour 1.33.5
* External DNS 0.21.0+vmware.2-vks.1
* ArgoDC 1.2.0
* VKSM Auto Attach 9.1.1
* Supervisor Management Proxy 9.1.1
VMware vSphere Supervisor LCI 9.1.2

In addition to the components and services above, the MPC also includes the following VCF Services:
* Migration Service Engine 9.1.1
* Migration Service 9.1.1
* ArgoCD 1.2.0
* Configuration Service 9.1.1
* Data Services 9.1.1
* Encryption Management 9.1.1
* Metrics Aggregator 9.1.1
* Protection and Recovery 9.1.1
* Harbor 9.1.1
* Secret Store 9.1.1

In addition to the components and services above, the MPC also includes the following add-ons:
* VMware Data Services Manager 9.1.1
* Protection and Recovery 9.1.1

The MPC design must provide the following elements using standard technical writing practices:
* Architect-Level: Conceptual designs, descriptions of each component and service, and their dependencies
* Engineering-Level: Logical designs, relationships between each component and service, integration points, and their prerequisites
* Operations-Level: Functional designs, step by step instructions needed to implement the entire solution across networking, compute, storage, and shared services (DNS, AD, etc)
* Automation-Level: APIs and CRUD operators, preferred python and PowerCLI.

# Customer Discovery

<!-- Each discovery element must capture a requirement, a requirement owner, and
     the date the requirement was captured. The owner must not be the architect or
     a reviewer, and the requirement text must be the owner's own words, verbatim,
     unedited. -->

| Requirement | Owner | Date Captured |
|---|---|---|



