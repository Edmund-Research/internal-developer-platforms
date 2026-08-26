# 03 – Target State

> **Project Fortress**
> **Initiative 1 – Know Your Platform**

---

# Purpose

This document defines the desired future state for Acme Corp's software inventory and service discovery capabilities.

It establishes the operating model, architectural principles, and measurable outcomes that will guide the implementation of Initiative 1.

Rather than introducing another documentation system, the objective is to establish a trusted operational data source that becomes the foundation of the Internal Developer Platform.

---

# Vision

Acme Corp will maintain a **living Software Catalog** that automatically represents every production software asset.

The catalog will become the authoritative source of truth for engineering metadata, enabling developers, platform engineers, security teams, and site reliability engineers to discover, understand, and operate services through a single interface.

The catalog will evolve from a passive inventory into an active platform capability that supports automation, governance, reliability, and developer experience.

---

# Future Operating Model

Following implementation, software metadata will no longer be managed manually.

Instead, metadata will become part of the software delivery lifecycle.

Every service created, deployed, modified, or retired will automatically update its representation within the Software Catalog.

Operational knowledge becomes continuously synchronized rather than periodically documented.

```text
Developer Creates Service
           │
           ▼
Golden Path Template
           │
           ▼
Metadata Generated
           │
           ▼
Source Repository
           │
           ▼
Software Catalog
           │
           ▼
Platform Capabilities
```

Although Golden Path templates are introduced in the next Fortress initiative, this operating model establishes the long-term direction.

---

# Guiding Principles

The following principles govern every design decision made during Initiative 1.

## Principle 1 – The Catalog Is the Source of Truth

The Software Catalog becomes the authoritative inventory of engineering assets.

Other systems may consume metadata, but they should not become competing sources of operational truth.

---

## Principle 2 – Metadata Is Code

Metadata should be version controlled alongside the software it describes.

Every service must define its metadata declaratively.

Changes to ownership, lifecycle, APIs, and documentation should follow the same review process as application code.

---

## Principle 3 – Automation Before Administration

Manual catalog maintenance does not scale.

Every opportunity to automate service registration, metadata validation, and synchronization should be prioritized over manual operational processes.

---

## Principle 4 – Ownership Is Mandatory

Every production service must have an accountable owner.

Ownership metadata is not optional.

Services without owners represent operational risk.

---

## Principle 5 – Documentation Should Be Discoverable

Documentation should not depend on institutional knowledge.

The Software Catalog should provide direct access to:

* architecture documentation
* operational runbooks
* dashboards
* APIs
* repositories
* SLOs

---

## Principle 6 – Platform Metadata Enables Platform Automation

Every future Fortress capability depends on trusted metadata.

The Software Catalog therefore becomes a foundational platform service rather than an isolated developer portal.

---

# Target Capabilities

At the completion of Initiative 1, the platform will provide the following capabilities.

## Centralized Software Inventory

Every production asset is represented as a catalog entity.

Supported entity types include:

* Services
* APIs
* Libraries
* Systems
* Resources
* Components
* Engineering Teams
* Domains

---

## Standardized Metadata

Every catalog entity includes consistent metadata.

Required attributes include:

* service name
* description
* owner
* engineering team
* lifecycle
* repository
* deployment environment
* Kubernetes namespace
* documentation
* runbooks
* monitoring
* SLO references

---

## Automated Registration

Services are registered automatically during onboarding or deployment.

Manual catalog creation should become the exception rather than the standard process.

---

## Continuous Synchronization

Catalog information remains synchronized with operational systems.

Synchronization detects:

* new services
* retired services
* ownership changes
* stale metadata
* missing documentation

---

## Metadata Validation

Platform policies validate required metadata before catalog publication.

Validation prevents incomplete or inconsistent service records from entering the catalog.

---

## Catalog Health Reporting

Platform Engineering can continuously measure:

* catalog completeness
* ownership coverage
* documentation coverage
* metadata freshness
* synchronization success

---

# Target Architecture

The Software Catalog becomes the central metadata platform for Fortress.

```text
                     Source Code
                          │
                          ▼
                 catalog-info.yaml
                          │
                          ▼
                  Software Catalog
                          │
      ┌─────────────┬──────────────┬──────────────┐
      │             │              │              │
      ▼             ▼              ▼              ▼
 Kubernetes      Documentation   Monitoring    Platform APIs
      │             │              │              │
      └─────────────┴──────────────┴──────────────┘
                          │
                          ▼
               Internal Developer Platform
```

Every future platform capability consumes metadata from the Software Catalog instead of maintaining its own inventory.

---

# Operational Workflow

The desired operational workflow becomes:

1. Developer creates or updates a service.
2. Metadata is committed alongside application code.
3. Validation policies verify metadata quality.
4. Catalog synchronization publishes changes.
5. Platform dashboards update automatically.
6. Service becomes discoverable across the organization.

No manual Platform Engineering intervention is required.

---

# Success Criteria

Initiative 1 will be considered complete when the following outcomes are achieved.

| Objective                                  |     Target |
| ------------------------------------------ | ---------: |
| Production services represented in catalog |       100% |
| Verified ownership                         |       100% |
| Source repositories linked                 |       100% |
| Documentation linked                       |       ≥95% |
| Automated synchronization                  |    Enabled |
| Metadata validation                        |   Enforced |
| Manual catalog updates                     | Eliminated |
| Catalog accuracy                           |       ≥98% |

---

# Non-Goals

This initiative intentionally excludes several capabilities that will be delivered later in Project Fortress.

These include:

* service scaffolding
* deployment automation
* infrastructure provisioning
* GitOps workflows
* secrets management
* policy enforcement
* cost management
* developer analytics

The objective of Initiative 1 is to establish trusted metadata—not to solve every platform engineering challenge simultaneously.

---

# Expected Organizational Outcomes

Following implementation, engineers should be able to answer the following questions within seconds.

* Who owns this service?
* Where is it deployed?
* Which repository contains its source code?
* Which APIs does it expose?
* Which Kubernetes namespace hosts it?
* Where are its dashboards?
* What SLO governs it?
* Where are its operational runbooks?

Operational discovery becomes self-service.

---

# Risks and Mitigations

| Risk                                | Mitigation                                                                         |
| ----------------------------------- | ---------------------------------------------------------------------------------- |
| Developers neglect metadata updates | Validate metadata in CI and during catalog synchronization.                        |
| Catalog becomes outdated            | Implement automated synchronization from source repositories and platform systems. |
| Inconsistent metadata quality       | Enforce validation policies and standardized templates.                            |
| Low developer adoption              | Integrate catalog creation into Golden Path templates in Initiative 2.             |
| Duplicate entities                  | Implement entity validation and ownership rules.                                   |

---

# Strategic Impact

The Software Catalog is more than an inventory of services.

It becomes the operational backbone of the Internal Developer Platform.

Future Fortress initiatives—including deployment automation, self-service infrastructure, platform observability, governance, and analytics—will consume this shared metadata rather than maintaining independent service registries.

By establishing a trusted source of operational truth now, Acme Corp creates the conditions necessary for scalable platform automation.

---

# Decision Record

## Decision ID

**FORTRESS-I1-ADR-001**

### Title

Adopt a centralized Software Catalog as the authoritative source of engineering metadata.

### Status

Approved

### Context

Operational metadata is fragmented across repositories, Kubernetes clusters, documentation systems, and team knowledge.

This fragmentation prevents automation, governance, and reliable service discovery.

### Decision

Acme Corp will adopt a centralized Software Catalog as the authoritative registry for all engineering assets.

Metadata will be managed declaratively alongside application code and synchronized automatically with platform systems.

### Consequences

**Positive**

* Establishes a single source of truth.
* Enables future platform automation.
* Improves discoverability.
* Strengthens governance.
* Reduces manual administration.

**Trade-offs**

* Engineering teams must maintain metadata as part of normal development.
* Platform automation must continuously validate and synchronize catalog information.
* Platform Engineering assumes ownership of catalog availability and integrity.

### Related Initiatives

* Initiative 2 – Golden Paths
* Initiative 4 – Deployment Platform
* Initiative 6 – Platform Observability
* Initiative 8 – Platform Governance

These initiatives directly depend on the architectural direction established by this decision.

---

# Transition to Architecture

With the target operating model now defined, the next document specifies the technical architecture required to realize this vision.

It identifies the platform components, their responsibilities, integration points, deployment topology, and operational data flows that collectively implement the Software Catalog capability within Project Fortress.
