# 04 – Architecture

> **Project Fortress**
> **Initiative 1 – Know Your Platform**

---

# Purpose

This document defines the technical architecture for Initiative 1 of Project Fortress.

Its objective is to establish a Software Catalog that serves as the authoritative source of engineering metadata across Acme Corp.

The architecture emphasizes automation, discoverability, standardization, and operational reliability while providing a scalable foundation for future Internal Developer Platform capabilities.

---

# Architecture Objectives

The proposed architecture must:

* establish a single source of truth for engineering metadata
* minimize manual administration
* integrate with existing engineering workflows
* support future platform automation
* remain highly available
* scale with organizational growth
* expose standardized metadata for downstream platform services

---

# Architectural Principles

## Source of Truth

The Software Catalog is the authoritative inventory of software assets.

No downstream platform capability should maintain an independent inventory of services.

---

## Declarative Metadata

Engineering metadata is defined as code and version-controlled alongside the application it describes.

Metadata changes follow the same review and approval workflow as software changes.

---

## Automation by Default

Catalog entities are discovered, validated, and synchronized automatically wherever possible.

Manual intervention should be reserved for exceptional cases.

---

## Loose Coupling

The Software Catalog consumes metadata from engineering systems but does not tightly couple those systems together.

Each component maintains a clearly defined responsibility.

---

## Extensibility

The architecture must support future integrations with:

* Argo CD
* Crossplane
* External Secrets
* Prometheus
* Grafana
* Vault
* Policy engines
* Internal deployment services

without requiring architectural redesign.

---

# Logical Architecture

```text
                        +----------------------+
                        |     Git Repository   |
                        |  catalog-info.yaml   |
                        +----------+-----------+
                                   |
                                   |
                                   v
                    +-------------------------------+
                    | Metadata Validation Pipeline  |
                    +---------------+---------------+
                                    |
                                    v
                     +------------------------------+
                     |       Backstage Catalog      |
                     | Authoritative Metadata Store |
                     +------+------------+----------+
                            |            |
          +-----------------+            +------------------+
          |                                         |
          v                                         v
+-----------------------+                +------------------------+
| Kubernetes Discovery  |                | Documentation Sources  |
+-----------+-----------+                +-----------+------------+
            |                                        |
            +-------------------+--------------------+
                                |
                                v
                    +------------------------------+
                    | Internal Developer Platform  |
                    |   Consumers of Metadata      |
                    +------------------------------+
```

The Software Catalog acts as the central metadata aggregation layer rather than an application deployment platform.

---

# Component Responsibilities

## Backstage

Responsible for:

* catalog storage
* service discovery
* entity relationships
* developer portal
* metadata presentation

Backstage does **not** provision infrastructure or deploy applications during this initiative.

---

## Git Repository

Responsible for:

* metadata ownership
* version control
* peer review
* audit history

Each service repository contains a `catalog-info.yaml` file describing the service.

---

## Validation Pipeline

Responsible for:

* metadata schema validation
* ownership enforcement
* duplicate detection
* lifecycle validation

Only compliant metadata enters the Software Catalog.

---

## Kubernetes Discovery

Responsible for:

* discovering deployed workloads
* validating deployment metadata
* identifying orphaned workloads
* supporting catalog synchronization

---

## Documentation Platform

Responsible for:

* technical documentation
* operational runbooks
* API references
* onboarding guides

Documentation remains distributed but is indexed through the Software Catalog.

---

# Metadata Lifecycle

```text
Developer
    │
    ▼
Update catalog-info.yaml
    │
    ▼
Pull Request
    │
    ▼
Validation Pipeline
    │
    ▼
Merge
    │
    ▼
Catalog Synchronization
    │
    ▼
Backstage Catalog Updated
    │
    ▼
Platform Consumers Refreshed
```

This lifecycle ensures that metadata evolves alongside the software itself.

---

# Integration Architecture

The Software Catalog integrates with existing engineering systems without replacing them.

| System        | Integration Purpose  |
| ------------- | -------------------- |
| Git           | Metadata source      |
| Kubernetes    | Workload discovery   |
| Documentation | Knowledge discovery  |
| Monitoring    | Dashboard references |
| CI/CD         | Metadata validation  |
| Future GitOps | Deployment metadata  |

---

# Security Architecture

The Software Catalog does not become the source of sensitive operational data.

Sensitive information remains within dedicated systems.

The catalog stores references rather than secrets.

Examples include:

* repository URLs
* dashboard links
* documentation links
* namespace identifiers
* ownership metadata

The following information is explicitly excluded:

* passwords
* API keys
* certificates
* database credentials
* tokens

Secret management is introduced in Initiative 5.

---

# Availability Considerations

The Software Catalog becomes a critical platform service.

To support operational reliability:

* Backstage should be deployed redundantly
* catalog data should be backed by persistent storage
* synchronization jobs should be idempotent
* validation failures should not corrupt catalog state
* monitoring should detect synchronization failures

---

# Scalability

The architecture should comfortably support:

* hundreds of engineering teams
* thousands of services
* multiple Kubernetes clusters
* multiple deployment environments
* future cloud providers

Horizontal scalability is preferred over manual operational expansion.

---

# Operational Model

Platform Engineering owns:

* Backstage platform
* validation policies
* synchronization workflows
* catalog standards

Engineering teams own:

* service metadata
* ownership information
* documentation
* lifecycle status

This separation reinforces the platform-as-a-product model while preserving service ownership within delivery teams.

---

# Risks

| Risk                   | Mitigation                                            |
| ---------------------- | ----------------------------------------------------- |
| Metadata becomes stale | Automated synchronization and validation              |
| Missing ownership      | Mandatory metadata enforcement                        |
| Duplicate entities     | Entity validation policies                            |
| Low adoption           | Integrate catalog creation into Golden Path templates |
| Platform outage        | Highly available Backstage deployment                 |

---

# Trade-offs

| Decision                     | Benefit                 | Trade-off                                    |
| ---------------------------- | ----------------------- | -------------------------------------------- |
| Metadata stored in Git       | Versioned and auditable | Requires developer discipline                |
| Backstage as central catalog | Unified discovery       | Additional platform component                |
| Automated synchronization    | Reduces manual effort   | Requires reliable automation                 |
| Distributed documentation    | Teams retain ownership  | Documentation quality still depends on teams |

---

# Architecture Decision Record 002

## Title

Adopt Backstage as the metadata aggregation platform.

### Context

Acme Corp requires a centralized engineering portal capable of representing services, APIs, teams, documentation, and future platform integrations.

### Decision

Backstage will serve as the presentation and catalog layer for Project Fortress.

### Rationale

* CNCF ecosystem alignment
* Extensible plugin model
* Strong software catalog capabilities
* Broad industry adoption
* Integration with future platform services

---

# Architecture Decision Record 003

## Title

Store service metadata alongside application code.

### Context

Separate metadata repositories frequently become outdated.

### Decision

Every service repository will contain a `catalog-info.yaml` file managed through normal software development workflows.

### Consequences

Metadata benefits from version control, peer review, traceability, and automated validation while remaining closely aligned with the software it describes.

---

# Architecture Summary

The Initiative 1 architecture establishes a metadata platform rather than an infrastructure platform.

By separating metadata ownership from platform ownership, Acme Corp gains a scalable, discoverable, and automatable inventory of engineering assets without disrupting existing software delivery practices.

This architecture provides the foundation required for every subsequent Fortress initiative, enabling the Internal Developer Platform to build upon a trusted source of engineering truth rather than fragmented operational knowledge.
