# Product & Scope

The LMS is a reusable enterprise control plane for current and future AI products. It centralizes customer/site/device management, licensing, entitlement pools, Marketplace/OTA, model lifecycle, capacity planning, renewal, audit and offline operations.

## Primary actors

- Vendor Super Admin
- Product Admin
- Release Manager
- Security Approver
- Developer
- Support Engineer
- Customer Admin
- Site Admin
- Read-Only Auditor
- Edge Device / Server

~~~mermaid
flowchart TD
    C[Customer / Organization] --> S1[Site A]
    C --> S2[Site B]
    C --> D[Owned Devices / Servers]
    D --> A1[Device-to-Site Assignment]
    A1 --> S1
    A1 --> S2
~~~

A device belongs commercially to a customer but may serve one or more sites.