# Initiative 1: Know Your Platform

> **Project Fortress**
> *Building Acme Corp's Internal Developer Platform*

---

## Executive Summary

As Acme Corp has scaled to more than **150 microservices** across multiple Kubernetes clusters, engineering teams have gradually lost visibility into the software ecosystem they maintain. Service ownership is inconsistent, documentation is incomplete, deployments are difficult to trace, and operational knowledge is distributed across tribal knowledge, spreadsheets, and messaging platforms.

These gaps have introduced significant operational risk. Platform engineers spend valuable time answering questions such as:

* Who owns this service?
* Where is it deployed?
* Which repository contains its source code?
* Does it have an SLO?
* Is it monitored?
* Who should respond when it fails?

Without a reliable inventory of platform assets, every reliability initiative becomes reactive rather than proactive.

The first initiative of **Project Fortress** establishes a **Software Catalog** as the authoritative inventory of every application, service, API, library, infrastructure component, and engineering team operating within Acme Corp.

Rather than treating documentation as an afterthought, Fortress integrates service discovery directly into the software delivery lifecycle. Every production workload becomes discoverable, owned, documented, and measurable.

This initiative lays the foundation upon which every subsequent Fortress capability will depend.

---

# Business Context

The Platform Engineering team has been tasked with improving developer experience while increasing the operational reliability of Acme Corp's Internal Developer Platform.

However, before self-service infrastructure, standardized deployments, or golden path templates can be introduced, the organization must answer one fundamental question:

> **What exactly are we operating?**

Without an accurate inventory of software assets, it is impossible to:

* establish ownership
* define service level objectives
* automate deployments
* measure platform adoption
* enforce governance policies
* understand dependencies
* identify technical debt

This initiative addresses that challenge by introducing a centralized Software Catalog powered by Backstage.

---

# Initiative Objectives

Upon completion of this initiative, Acme Corp will have a platform capable of:

* Automatically discovering production services
* Registering services within a centralized software catalog
* Enforcing mandatory ownership metadata
* Associating services with Git repositories
* Linking services to Kubernetes workloads
* Associating operational dashboards and runbooks
* Tracking Service Level Objectives
* Detecting stale or orphaned catalog entries
* Providing a single source of truth for engineering assets

---

# Scope

This initiative focuses exclusively on establishing platform visibility.

Included:

* Software Catalog
* Backstage deployment and configuration
* Catalog entity templates
* Metadata validation
* Automatic catalog synchronization
* Catalog health reporting
* Service ownership enforcement

Out of scope:

* Service scaffolding
* CI/CD pipelines
* Deployment automation
* Infrastructure provisioning
* Secret management
* Policy enforcement
* Developer portals beyond catalog functionality

These capabilities will be introduced in subsequent Fortress initiatives.

---

# Architecture Overview

```
                        Git Repositories
                               │
                               │
                     catalog-info.yaml
                               │
                               ▼
                     ┌───────────────────┐
                     │     Backstage     │
                     │ Software Catalog  │
                     └─────────┬─────────┘
                               │
          ┌────────────────────┼─────────────────────┐
          │                    │                     │
          ▼                    ▼                     ▼
 Kubernetes Clusters      Engineering Teams     Documentation

          │                    │                     │
          └────────────────────┼─────────────────────┘
                               │
                               ▼
                    Platform Engineering
```

The Software Catalog becomes the operational control plane for platform metadata.

Future Fortress initiatives will integrate with this catalog rather than creating separate inventories.

---

# Deliverables

This initiative produces the following artifacts.

```
know-your-platform/

├── README.md
├── 01-business-problem.md
├── 02-current-state.md
├── 03-target-state.md
├── 04-architecture.md
├── 05-implementation.md
├── 06-demo.md
├── 07-success-metrics.md
├── 08-lessons-learned.md
│
├── assets/
│
├── diagrams/
│
├── configs/
│   ├── backstage-app-config.yaml
│   ├── catalog-info-template.yaml
│   ├── entity-validation-policy.yaml
│   └── catalog-sync-cronjob.yaml
│
├── scripts/
│   ├── catalog-accuracy-report.sh
│   ├── stale-entity-detector.py
│   └── ownership-validator.sh
│
└── runbooks/
    ├── catalog-sync.md
    ├── onboarding.md
    └── troubleshooting.md
```

Each artifact contributes to a production-ready implementation rather than serving as a standalone tutorial.

---

# Success Criteria

The initiative will be considered successful when the following objectives are achieved:

| Objective                              | Target     |
| -------------------------------------- | ---------- |
| Services registered                    | 100%       |
| Services with owners                   | 100%       |
| Services linked to source repositories | 100%       |
| Services with documentation            | ≥95%       |
| Automatic catalog synchronization      | Enabled    |
| Stale catalog entries                  | <2%        |
| Manual catalog maintenance             | Eliminated |

---

# Expected Business Outcomes

Following implementation, Acme Corp should realize measurable improvements across several dimensions.

### Improved Operational Visibility

Platform engineers can immediately identify ownership, deployment location, documentation, and operational metadata for every production service.

### Reduced Operational Risk

Unknown or orphaned services become visible and actionable before they become operational liabilities.

### Faster Incident Response

Engineers no longer spend valuable incident time determining who owns an affected service.

### Improved Governance

Mandatory metadata creates the foundation for future policy enforcement.

### Reduced Cognitive Load

Developers spend less time searching for service information and more time delivering business value.

---

# Dependencies

This initiative intentionally minimizes external dependencies.

Primary platform components include:

* Kubernetes
* Backstage
* Git repositories
* Service metadata
* Catalog synchronization workflows

Subsequent initiatives will integrate additional platform capabilities including GitOps, Crossplane, Vault, Argo CD, Prometheus, Grafana, and policy engines.

---

# Relationship to Future Fortress Initiatives

This initiative establishes the operational foundation upon which every subsequent Fortress capability depends.

The Software Catalog becomes the authoritative inventory consumed by:

* Initiative 2 – Golden Paths
* Initiative 3 – Self-Service Infrastructure
* Initiative 4 – Deployment Platform
* Initiative 5 – Secrets Platform
* Initiative 6 – Platform Observability
* Initiative 7 – Platform Reliability
* Initiative 8 – Platform Governance
* Initiative 9 – Cost Visibility
* Initiative 10 – Developer Experience
* Initiative 11 – Platform Analytics
* Initiative 12 – Incident Readiness
* Initiative 13 – Platform Migration
* Initiative 14 – Platform Optimization

Without a trusted inventory of platform assets, none of these initiatives can reliably automate engineering workflows.

---

# Completion Criteria

This initiative concludes when Acme Corp can confidently answer the following questions for every production service:

* What is this service?
* Who owns it?
* Where is its source code?
* Where is it deployed?
* What does it depend on?
* How is it monitored?
* What SLO governs its reliability?
* Where is its operational documentation?
* Is its catalog information current?

Only after these questions can be answered consistently is the organization prepared to introduce self-service platform capabilities.

---

## Next Initiative

With a centralized Software Catalog established, Project Fortress proceeds to **Initiative 2 – Golden Paths**, where the Platform Engineering team standardizes how new services are created, onboarded, and integrated into the platform by default.

The Software Catalog developed in this initiative becomes the authoritative registry used by every subsequent platform capability.
