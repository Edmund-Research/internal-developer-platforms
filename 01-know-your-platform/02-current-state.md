# 02 – Current State Assessment

> **Project Fortress**
> **Initiative 1 – Know Your Platform**

---

# Purpose

Before implementing the first capability of Project Fortress, the Platform Engineering team conducted an assessment of Acme Corp's current software delivery landscape.

The objective of this assessment is to establish a factual baseline from which platform improvements can be measured throughout the Fortress program.

Rather than evaluating individual technologies, this assessment focuses on the organization's operational maturity, platform capabilities, and developer experience.

The findings documented here represent the state of the platform before any Fortress initiatives have been implemented.

---

# Executive Summary

Acme Corp has successfully adopted Kubernetes and microservices to support business growth. Engineering teams deploy applications independently and have significant autonomy over their tooling and delivery practices.

While this flexibility accelerated early development, it has resulted in an increasingly fragmented engineering ecosystem.

Operational information is scattered across multiple systems, engineering standards vary between teams, and platform processes rely heavily on manual coordination.

The Platform Engineering team currently operates in a reactive capacity, responding to infrastructure requests, onboarding support, and operational questions instead of delivering self-service platform capabilities.

Although the platform remains functional, its operational maturity has not kept pace with organizational growth.

---

# Current Platform Landscape

## Organization

| Area                | Current State          |
| ------------------- | ---------------------- |
| Engineering Teams   | 18                     |
| Microservices       | ~150                   |
| Kubernetes Clusters | Multiple               |
| CI/CD Platforms     | Mixed implementations  |
| Documentation       | Distributed            |
| Source Control      | Git                    |
| Monitoring          | Partially standardized |
| Platform Team       | Centralized            |

---

# Platform Capability Assessment

The Platform Engineering team evaluated key operational capabilities using a five-level maturity model.

| Level   | Description      |
| ------- | ---------------- |
| Level 1 | Initial / Ad Hoc |
| Level 2 | Developing       |
| Level 3 | Defined          |
| Level 4 | Managed          |
| Level 5 | Optimized        |

---

## Assessment Results

| Capability                  | Current Level | Observations                                              |
| --------------------------- | ------------- | --------------------------------------------------------- |
| Software Catalog            | 1             | No centralized inventory exists.                          |
| Service Ownership           | 2             | Ownership exists informally but is inconsistent.          |
| Documentation               | 2             | Documentation quality varies significantly between teams. |
| Deployment Standardization  | 2             | Teams maintain independent deployment processes.          |
| Infrastructure Provisioning | 1             | Platform team provisions infrastructure manually.         |
| Secret Management           | 2             | Mixed approaches across environments.                     |
| Platform Observability      | 2             | Limited visibility into platform health.                  |
| Reliability Engineering     | 1             | SLO adoption is minimal.                                  |
| Governance                  | 1             | Metadata standards are not enforced.                      |
| Cost Visibility             | 1             | Infrastructure costs are difficult to attribute.          |
| Developer Self-Service      | 1             | Most platform requests require manual intervention.       |
| Platform Analytics          | 1             | Developer experience metrics are not collected.           |

---

# Current Software Inventory

At present, no authoritative inventory of software assets exists.

Instead, service information is distributed across multiple locations.

```text
Git Repositories
        │
        ├────────────┐
        │            │
        ▼            ▼

 Kubernetes      Wiki Pages

        │            │

        └──────┬─────┘

               ▼

 Slack Conversations

               │

               ▼

 Tribal Knowledge
```

No single source contains:

* service ownership
* deployment locations
* lifecycle status
* operational documentation
* APIs
* dependencies
* monitoring links
* Service Level Objectives

As a result, engineers often reconstruct service information manually.

---

# Service Ownership

Ownership practices vary considerably across engineering teams.

Current observations include:

* some services have clearly defined owners
* others are maintained by entire teams
* ownership information is stored inconsistently
* historical services no longer have active maintainers
* on-call responsibilities are difficult to identify

This inconsistency introduces delays during operational incidents and platform changes.

---

# Documentation

Documentation practices are decentralized.

Current challenges include:

* outdated wiki pages
* inconsistent README quality
* undocumented APIs
* missing runbooks
* duplicate documentation
* documentation disconnected from deployments

Engineers frequently rely on experienced team members rather than written documentation.

---

# Deployment Practices

Engineering teams have developed independent deployment workflows over time.

Observed variations include:

* different branching strategies
* different CI/CD pipelines
* inconsistent deployment approvals
* varying rollback procedures
* inconsistent deployment notifications

These differences complicate operational support and reduce platform consistency.

---

# Infrastructure Provisioning

Infrastructure requests currently require Platform Engineering involvement.

Typical workflow:

```text
Developer

↓

Open Infrastructure Ticket

↓

Platform Review

↓

Manual Provisioning

↓

Validation

↓

Developer Notification
```

Average turnaround depends on request complexity and platform workload.

This process creates delivery bottlenecks and reduces engineering autonomy.

---

# Secret Management

Secret management practices vary across teams.

Examples include:

* manually created Kubernetes Secrets
* environment-specific credentials
* inconsistent rotation procedures
* varying access controls

No standardized self-service secret provisioning process currently exists.

---

# Observability

Observability tooling is available but adoption is inconsistent.

Current observations:

* some services expose Prometheus metrics
* dashboard quality varies
* alert ownership is inconsistent
* tracing adoption is limited
* service dependencies are difficult to visualize

Platform health itself is not comprehensively monitored.

---

# Reliability Practices

Reliability engineering practices remain in the early stages of adoption.

Current findings include:

* few documented SLOs
* inconsistent alerting thresholds
* reactive incident management
* varying operational maturity between teams

Reliability objectives are not consistently incorporated into service onboarding.

---

# Governance

Engineering standards exist but rely primarily on manual compliance.

Examples include:

* inconsistent metadata
* missing ownership labels
* varying naming conventions
* inconsistent lifecycle tracking

Without automated validation, governance depends heavily on individual engineering discipline.

---

# Developer Experience

Developers frequently interact with the Platform Engineering team for operational support.

Common requests include:

* Kubernetes namespaces
* deployment assistance
* secret creation
* infrastructure provisioning
* service onboarding
* documentation discovery

Many of these activities could ultimately become self-service capabilities.

---

# Operational Pain Points

The assessment identified several recurring themes.

## Fragmented Information

Operational knowledge is distributed across multiple systems.

## Manual Processes

Platform engineers perform repetitive operational work.

## Limited Discoverability

Finding service information requires multiple searches.

## Inconsistent Standards

Engineering teams implement similar capabilities differently.

## Reactive Operations

The Platform Engineering team spends more time responding to requests than improving the platform.

---

# Risks

If no improvements are made, Acme Corp is likely to experience:

* increasing operational complexity
* slower onboarding of engineers
* longer incident response times
* duplicated engineering effort
* higher platform maintenance costs
* increasing technical debt
* reduced engineering velocity

These risks will grow alongside the organization's software estate.

---

# Opportunities

Despite the current challenges, the assessment also identifies strong foundations.

Acme Corp already has:

* Kubernetes as a common runtime
* mature engineering teams
* Git-based development workflows
* centralized Platform Engineering ownership
* strong adoption of cloud-native technologies

These foundations make the organization well positioned to introduce an Internal Developer Platform.

---

# Baseline Metrics

The following metrics establish the baseline against which future Fortress initiatives will be evaluated.

| Metric                             | Baseline     |
| ---------------------------------- | ------------ |
| Catalog Coverage                   | 0%           |
| Services with Verified Owners      | Unknown      |
| Services with SLOs                 | <10%         |
| Automatic Service Registration     | No           |
| Manual Platform Requests           | High         |
| Platform Self-Service Capabilities | Minimal      |
| Developer Portal Adoption          | None         |
| Metadata Validation                | Manual       |
| Catalog Accuracy                   | Not Measured |

These values represent the starting point of the Fortress transformation journey.

---

# Assessment Summary

The Platform Engineering team concludes that Acme Corp's greatest challenge is not a lack of technical capability but a lack of centralized operational knowledge.

Engineering teams have successfully delivered software at scale, but the supporting platform has evolved organically rather than intentionally.

As a result, operational metadata has become fragmented, manual processes have accumulated, and platform complexity has increased.

The organization is now at an inflection point.

Further scaling without a centralized software catalog would increase operational overhead, reduce engineering efficiency, and limit the organization's ability to introduce future platform capabilities.

---

# Transition to the Target State

The next document defines the desired future state for Initiative 1.

It establishes the operating model, architectural principles, and success criteria for Acme Corp's Software Catalog, providing the blueprint that guides the implementation of the first Fortress capability.
