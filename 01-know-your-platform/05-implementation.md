# 05 – Implementation

> **Project Fortress**
> **Initiative 1 – Know Your Platform**

---

# Purpose

This document defines the implementation plan for the Software Catalog established in Initiative 1 of Project Fortress.

The implementation is designed as a progressive rollout that begins with a controlled pilot and expands to organization-wide adoption after the catalog model, metadata standards, automation, and operational processes have been validated.

The objective is not simply to deploy Backstage.

The objective is to establish a **reliable and sustainable service inventory** that Acme Corp can operate as a production platform capability.

---

# Implementation Objectives

The implementation must deliver:

* A production-capable Backstage deployment
* Standardized service metadata
* Automated metadata validation
* Git-based service registration
* Kubernetes workload discovery
* Catalog synchronization
* Ownership enforcement
* Catalog health reporting
* Operational monitoring
* Documentation and runbooks
* A repeatable onboarding process

---

# Implementation Strategy

The implementation follows four stages:

```text
Pilot
  │
  ▼
Department Rollout
  │
  ▼
Organization-Wide Adoption
  │
  ▼
Operationalization
```

Each stage has explicit entry criteria, deliverables, and exit criteria.

No stage begins until the previous stage has demonstrated sufficient stability.

---

# Implementation Roadmap

| Phase                         | Objective                                  | Primary Outcome                       |
| ----------------------------- | ------------------------------------------ | ------------------------------------- |
| 1. Pilot                      | Validate architecture and metadata model   | Working catalog for selected services |
| 2. Department Rollout         | Validate at team scale                     | Repeatable onboarding process         |
| 3. Organization-Wide Adoption | Catalog all production services            | ≥95% catalog coverage                 |
| 4. Operationalization         | Make catalog a managed platform capability | Sustainable ownership and reliability |

---

# Phase 1 – Pilot

## Objective

Validate the Software Catalog architecture using a small representative set of services.

The pilot should include services with different operational characteristics rather than selecting only simple applications.

Recommended pilot:

* 3–5 services
* at least two engineering teams
* at least two Kubernetes workloads
* at least one API
* at least one service with existing operational documentation
* at least one service with incomplete metadata

---

## Pilot Activities

### 1. Deploy Backstage

Deploy Backstage into the designated platform namespace.

The deployment should include:

* redundant application instances
* persistent catalog database
* Kubernetes integration
* Git integration
* authentication
* health checks
* resource limits
* observability

---

### 2. Establish Metadata Schema

Define the minimum metadata required for every service.

Example:

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: payments-api
  description: Acme payment processing API
  tags:
    - payments
    - api
spec:
  type: service
  lifecycle: production
  owner: team-payments
  system: payments
```

Additional operational metadata will be introduced as integrations mature.

---

### 3. Establish Ownership Model

Define how Acme Corp represents engineering teams.

Example:

```yaml
apiVersion: backstage.io/v1alpha1
kind: Group
metadata:
  name: team-payments
spec:
  type: team
  profile:
    displayName: Payments Engineering
  children: []
```

Ownership must use standardized team identifiers rather than free-form text.

---

### 4. Register Pilot Services

Each pilot service receives a `catalog-info.yaml`.

Example repository structure:

```text
payments-api/
├── src/
├── deployment/
├── docs/
├── README.md
└── catalog-info.yaml
```

---

### 5. Validate Metadata

The validation process must verify:

* entity syntax
* required fields
* valid owner
* valid lifecycle
* valid repository
* unique entity name

Invalid metadata must fail validation rather than silently entering the catalog.

---

### 6. Integrate Kubernetes Discovery

The platform discovers deployed workloads and correlates them with catalog entities.

The objective is to detect discrepancies such as:

```text
Catalog Service
       │
       └── payments-api
              │
              └── Kubernetes Deployment
                    └── payments-api

Result: Healthy
```

versus:

```text
Kubernetes Deployment
       │
       └── unknown-service

Result: Orphaned workload
```

---

## Pilot Exit Criteria

The pilot is complete when:

* all selected services appear in Backstage
* ownership is correctly represented
* repository links work
* Kubernetes relationships are visible
* metadata validation succeeds
* synchronization runs automatically
* catalog failures are observable
* onboarding can be repeated without Platform Engineering manually editing catalog records

---

# Phase 2 – Department Rollout

## Objective

Validate the platform with a larger number of engineering teams and services.

The pilot establishes technical viability.

The department rollout establishes **operational viability**.

---

## Scope

Expand the catalog to approximately:

* 5–7 engineering teams
* 30–50 services
* multiple repositories
* multiple Kubernetes namespaces

---

## Activities

### Standardize Onboarding

Create a documented onboarding workflow.

```text
Team Requests Onboarding
          │
          ▼
Platform Validates Repository
          │
          ▼
Metadata Added
          │
          ▼
Automated Validation
          │
          ▼
Catalog Registration
          │
          ▼
Team Verifies Service
```

---

### Measure Onboarding Effort

Track:

* onboarding duration
* number of Platform Engineering interventions
* validation failures
* metadata corrections
* synchronization failures

The goal is to progressively reduce manual intervention.

---

### Introduce Catalog Health Reporting

The Platform Engineering team begins publishing:

* catalog coverage
* ownership coverage
* stale entity count
* invalid entity count
* synchronization health

These measurements establish the first operational feedback loop.

---

## Department Rollout Exit Criteria

The rollout proceeds when:

* onboarding is repeatable
* teams can self-register services
* validation failures are actionable
* synchronization is stable
* catalog accuracy exceeds 95%
* no critical operational issues remain

---

# Phase 3 – Organization-Wide Adoption

## Objective

Register the complete Acme Corp production service estate.

The target is approximately:

**150+ services across 18 engineering teams.**

---

# Migration Strategy

The Platform Engineering team should avoid attempting to onboard every service simultaneously.

Services should be migrated in waves.

```text
Wave 1
Core Platform Services

        ↓

Wave 2
Customer-Facing Services

        ↓

Wave 3
Internal Services

        ↓

Wave 4
Legacy Services

        ↓

Wave 5
Remaining Exceptions
```

---

# Legacy Services

Legacy services represent a special case.

Some may lack:

* active maintainers
* documentation
* repositories
* standardized deployment metadata

These services should not simply be excluded.

Instead, they should be explicitly represented with a lifecycle such as:

```yaml
spec:
  lifecycle: deprecated
```

or:

```yaml
spec:
  lifecycle: experimental
```

The catalog should make technical debt visible rather than hiding it.

---

# Organization-Wide Exit Criteria

The organization-wide rollout is complete when:

* ≥95% of production services are cataloged
* 100% of cataloged production services have owners
* metadata validation is enforced
* synchronization is automated
* stale entities are measurable
* orphaned workloads are identifiable
* onboarding no longer requires manual catalog administration

---

# Phase 4 – Operationalization

## Objective

Transition the Software Catalog from an implementation project into a continuously managed platform capability.

---

# Platform Ownership

The Platform Engineering team owns:

* Backstage availability
* catalog architecture
* schema standards
* validation policies
* synchronization infrastructure
* operational monitoring
* platform documentation

Application teams own:

* service metadata
* service ownership
* documentation
* lifecycle status
* service-specific relationships

---

# Service-Level Expectations

The catalog itself becomes a platform dependency and therefore requires operational expectations.

Initial targets:

| Metric                     | Target       |
| -------------------------- | ------------ |
| Catalog availability       | ≥99.9%       |
| Synchronization success    | ≥99%         |
| Catalog coverage           | ≥98%         |
| Ownership coverage         | 100%         |
| Stale entities             | <2%          |
| Critical catalog incidents | 0 unresolved |

These targets become more formalized in Initiative 7 when Fortress establishes platform-wide SLOs.

---

# Deployment Architecture

The initial production deployment should use a Kubernetes-based architecture.

```text
                   Ingress
                      │
                      ▼
              +---------------+
              |   Backstage   |
              |   Instances   |
              +-------+-------+
                      │
          +-----------+-----------+
          │                       │
          ▼                       ▼
   Catalog Database        External Systems
          │                       │
          │              +--------+--------+
          │              │        │        │
          ▼              ▼        ▼        ▼
       Backup           Git    Kubernetes Docs
```

The catalog database must be persistent and backed up.

Backups must be tested rather than merely configured.

---

# Configuration Management

Backstage configuration must be version controlled.

Recommended structure:

```text
configs/
├── app-config.yaml
├── app-config.production.yaml
├── catalog/
│   ├── locations.yaml
│   ├── policies.yaml
│   └── templates.yaml
└── integrations/
    ├── git.yaml
    └── kubernetes.yaml
```

Environment-specific configuration should not contain secrets committed to Git.

Sensitive configuration must be injected through the platform's secret-management mechanism.

---

# CI Validation

Service metadata should be validated before merge.

Example workflow:

```text
Pull Request
     │
     ▼
catalog-info.yaml detected
     │
     ▼
Schema validation
     │
     ▼
Ownership validation
     │
     ▼
Repository validation
     │
     ▼
Entity uniqueness validation
     │
     ├── Failure → Pull Request blocked
     │
     ▼
Merge
```

This prevents invalid metadata from reaching the production catalog.

---

# Catalog Synchronization

Synchronization must be:

* automated
* repeatable
* idempotent
* observable

The synchronization process should not delete catalog entities solely because a transient upstream system is unavailable.

Instead:

```text
Upstream Failure
      │
      ▼
Sync Failure Recorded
      │
      ▼
Existing Catalog State Preserved
      │
      ▼
Alert Platform Team
      │
      ▼
Retry
```

This prevents temporary infrastructure failures from causing widespread metadata loss.

---

# Data Quality Controls

The catalog must continuously evaluate its own quality.

Minimum checks:

### Ownership

Every production service has a valid owner.

### Repository

Repository reference exists and remains accessible.

### Lifecycle

Lifecycle is one of the approved values.

### Documentation

Required documentation links exist.

### Deployment

Production services map to known workloads.

### Freshness

Metadata has been updated within the expected period.

---

# Failure Handling

The platform must distinguish between:

### Invalid Metadata

Example:

```text
Unknown owner: team-foo
```

Action:

Reject entity update.

---

### Temporary Integration Failure

Example:

```text
Git provider unavailable
```

Action:

Retain known-good catalog state and retry.

---

### Orphaned Workload

Example:

```text
Kubernetes deployment exists
but no matching catalog entity.
```

Action:

Report discrepancy for investigation.

---

### Stale Entity

Example:

```text
Service has not reported activity
within defined threshold.
```

Action:

Flag entity for owner review.

---

# Rollback Strategy

Backstage application changes must be deployable through the same release mechanism used by other production platform services.

Rollback must support:

* previous application version
* previous configuration
* database recovery where necessary

Catalog metadata should remain independently recoverable from its source repositories.

This separation ensures that an application rollback does not require manual reconstruction of service metadata.

---

# Testing Strategy

The implementation requires several layers of validation.

## Unit Testing

Validate:

* metadata parsers
* validation rules
* synchronization logic
* reporting scripts

---

## Integration Testing

Validate:

* Backstage ↔ Git
* Backstage ↔ Kubernetes
* catalog synchronization
* entity relationships

---

## Failure Testing

Simulate:

* Git outage
* Kubernetes API outage
* invalid metadata
* duplicate entities
* missing ownership
* deleted repositories
* stale services

---

## Recovery Testing

Verify:

* Backstage restart
* database restoration
* synchronization recovery
* failed job retry
* catalog consistency after recovery

---

# Observability

The platform should expose metrics for:

* catalog ingestion rate
* synchronization duration
* synchronization failures
* entity validation failures
* catalog entity count
* stale entities
* orphaned workloads
* API latency
* application availability

Logs should include correlation information sufficient to trace an entity from source repository to catalog registration.

---

# Security Controls

The implementation must enforce:

* authenticated Backstage access
* role-based access where required
* TLS for external communication
* least-privilege Kubernetes access
* read-only access to Kubernetes where possible
* no secrets in catalog metadata
* auditability of administrative changes

The Kubernetes integration should have only the permissions required to discover workloads.

---

# Operational Runbooks

The implementation must include runbooks covering:

* catalog synchronization failure
* invalid entity registration
* orphaned workload investigation
* stale entity remediation
* Backstage outage
* database recovery
* service onboarding

These runbooks become part of the operational deliverables for Initiative 1.

---

# Implementation Risks

| Risk                                | Impact | Mitigation                              |
| ----------------------------------- | ------ | --------------------------------------- |
| Low adoption                        | High   | Progressive rollout and team onboarding |
| Poor metadata quality               | High   | Automated validation                    |
| Synchronization failures            | High   | Retry and observability                 |
| Backstage outage                    | Medium | Redundant deployment                    |
| Catalog becomes stale               | High   | Automated freshness checks              |
| Legacy services cannot be onboarded | Medium | Explicit exception/lifecycle handling   |

---

# Implementation Definition of Done

Initiative 1 implementation is complete only when all of the following are true:

### Platform

* [ ] Backstage deployed
* [ ] Authentication configured
* [ ] Persistent catalog database configured
* [ ] Backups configured and tested
* [ ] Health checks configured
* [ ] Monitoring configured

### Metadata

* [ ] Standard entity schema defined
* [ ] Ownership model defined
* [ ] Lifecycle model defined
* [ ] Required metadata enforced

### Automation

* [ ] Git integration configured
* [ ] Kubernetes discovery configured
* [ ] Automatic synchronization enabled
* [ ] Synchronization failures observable

### Quality

* [ ] Duplicate detection implemented
* [ ] Ownership validation implemented
* [ ] Stale entity detection implemented
* [ ] Catalog accuracy reporting implemented

### Operations

* [ ] Runbooks completed
* [ ] Recovery procedures tested
* [ ] Onboarding process documented
* [ ] Platform ownership assigned

### Adoption

* [ ] Pilot completed
* [ ] Department rollout completed
* [ ] Organization-wide migration completed
* [ ] ≥95% production catalog coverage achieved

---

# Implementation Principles

The implementation should preserve several important characteristics of the target architecture.

### Fail Safely

Temporary failures must not destroy known-good catalog state.

### Automate Repetition

Anything Platform Engineering performs repeatedly should be considered a candidate for automation.

### Make Exceptions Visible

Unsupported or legacy services should be represented explicitly rather than silently excluded.

### Prefer Reversibility

Implementation decisions should allow components to be replaced or rolled back without requiring a platform-wide redesign.

### Measure Before Optimizing

Baseline metrics must be collected before declaring the platform successful.

---

# Handoff to Operations

After organization-wide adoption, ownership transitions from an implementation workstream into normal Platform Engineering operations.

The operational team assumes responsibility for:

* availability
* catalog accuracy
* synchronization health
* metadata standards
* onboarding support
* incident response
* continuous improvement

The catalog is now treated as a production platform service.

---

# Transition to Demonstration

The next document provides an end-to-end demonstration of the completed capability.

The demonstration will follow a real developer journey—from discovering an existing service, through ownership and operational metadata, to identifying a catalog discrepancy and resolving it.

The objective is to prove that the Software Catalog provides measurable operational value rather than simply demonstrating that Backstage is running.
