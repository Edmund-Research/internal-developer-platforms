# 06 – Demonstration & Acceptance Test

> **Project Fortress**
> **Initiative 1 – Know Your Platform**

---

# Purpose

This document defines the end-to-end demonstration and acceptance test for Initiative 1: **Know Your Platform**.

The demonstration validates that Acme Corp's Software Catalog is not merely deployed, but provides the operational capabilities defined by the initiative.

The demonstration follows a realistic developer and Platform Engineering workflow.

It should be executable against the deployed Fortress environment after implementation is complete.

---

# Demonstration Objective

At the end of this demonstration, we must be able to prove that:

1. A service can be represented in the Software Catalog.
2. Service ownership is explicit.
3. Repository information is discoverable.
4. Operational metadata is accessible.
5. Kubernetes workloads can be associated with catalog entities.
6. Invalid metadata is rejected.
7. Catalog synchronization operates automatically.
8. Orphaned workloads can be detected.
9. Stale catalog entities can be identified.
10. Catalog health can be measured.

The demonstration therefore tests both the **happy path** and important failure scenarios.

---

# Demonstration Environment

The demonstration requires:

| Component           | Purpose                      |
| ------------------- | ---------------------------- |
| Backstage           | Software Catalog             |
| Kubernetes          | Runtime discovery            |
| Git repository      | Metadata source              |
| PostgreSQL          | Catalog persistence          |
| Validation pipeline | Metadata quality enforcement |
| Synchronization job | Automated catalog updates    |
| Reporting scripts   | Catalog health measurement   |

The demonstration environment should be isolated from production workloads.

---

# Demonstration Scenario

The scenario uses a fictional Acme Corp service:

> **payments-api**

The service represents a typical production application owned by the Payments Engineering team.

The service will be used throughout the demonstration to validate the complete metadata lifecycle.

---

# Scenario 1 – Discover an Existing Service

## Objective

Demonstrate that a developer can locate an existing service without contacting Platform Engineering.

### Action

Open the Software Catalog and search for:

```text
payments-api
```

### Expected Result

The catalog displays:

* Service name
* Description
* Owner
* Lifecycle
* Repository
* System
* APIs
* Documentation
* Kubernetes deployment information

### Acceptance Criteria

* [ ] Service is discoverable by name.
* [ ] Service description is displayed.
* [ ] Owner is displayed.
* [ ] Lifecycle is displayed.
* [ ] Repository link is valid.
* [ ] Documentation link is available.

---

# Scenario 2 – Identify Service Ownership

## Objective

Demonstrate that an engineer can determine who owns a service.

### Action

Open the `payments-api` entity.

Navigate to the ownership information.

### Expected Result

The catalog identifies:

```text
Owner:
Payments Engineering

Team:
team-payments
```

### Acceptance Criteria

* [ ] Owner is present.
* [ ] Owner maps to a valid catalog Group.
* [ ] Team information is discoverable.
* [ ] Ownership does not depend on free-form text.

---

# Scenario 3 – Locate Operational Documentation

## Objective

Demonstrate that the catalog provides a central discovery point for operational information.

### Action

From the `payments-api` entity, locate:

* README
* Architecture documentation
* Runbook
* Dashboard
* API documentation

### Expected Result

The developer can navigate directly to the relevant resources.

### Acceptance Criteria

* [ ] Documentation links are present.
* [ ] Links resolve successfully.
* [ ] Runbook is discoverable.
* [ ] Monitoring dashboard is discoverable.

---

# Scenario 4 – Inspect Kubernetes Deployment

## Objective

Demonstrate that the Software Catalog can associate a service with its deployed workload.

### Action

Inspect the Kubernetes information for `payments-api`.

### Expected Result

The catalog identifies the relevant:

```text
Cluster
Namespace
Deployment
Pod
```

Example:

```text
Cluster: acme-prod-east
Namespace: payments
Deployment: payments-api
```

### Acceptance Criteria

* [ ] Kubernetes integration is operational.
* [ ] Deployment is associated with the correct catalog entity.
* [ ] Namespace is displayed.
* [ ] Cluster information is available.
* [ ] No credentials or secrets are exposed.

---

# Scenario 5 – Register a New Service

## Objective

Demonstrate the declarative registration workflow.

### Action

Create the following metadata file in a service repository:

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component

metadata:
  name: orders-api
  description: Acme order management API

spec:
  type: service
  lifecycle: production
  owner: team-orders
  system: commerce
```

Commit the change and open a pull request.

### Expected Result

The CI validation process evaluates the metadata.

If valid, the pull request is allowed to proceed.

After merge, the synchronization process discovers the entity.

### Acceptance Criteria

* [ ] Metadata is version controlled.
* [ ] Pull request validation executes.
* [ ] Valid metadata passes.
* [ ] Merged metadata is synchronized automatically.
* [ ] `orders-api` appears in the catalog.

---

# Scenario 6 – Reject Invalid Metadata

## Objective

Demonstrate that the platform prevents invalid catalog entities.

### Action

Modify the metadata:

```yaml
spec:
  type: service
  lifecycle: production
  owner: team-does-not-exist
```

Submit the change.

### Expected Result

Validation fails because the referenced owner does not exist.

Example:

```text
Validation failed:
Unknown owner: team-does-not-exist
```

### Acceptance Criteria

* [ ] Invalid metadata is detected automatically.
* [ ] Pull request validation fails.
* [ ] Error message identifies the problem.
* [ ] Invalid metadata cannot silently enter the catalog.

---

# Scenario 7 – Detect Duplicate Entities

## Objective

Demonstrate that entity uniqueness is enforced.

### Action

Create a second catalog entity using an existing name:

```yaml
metadata:
  name: payments-api
```

### Expected Result

The validation process detects the duplicate entity.

Example:

```text
Validation failed:
Entity payments-api already exists.
```

### Acceptance Criteria

* [ ] Duplicate entity is detected.
* [ ] Existing catalog state remains unchanged.
* [ ] Developer receives an actionable error.

---

# Scenario 8 – Detect an Orphaned Kubernetes Workload

## Objective

Demonstrate that the platform can identify workloads that are not represented in the catalog.

### Action

Deploy a Kubernetes workload:

```text
inventory-worker
```

without creating a corresponding catalog entity.

### Expected Result

The synchronization process detects:

```text
Orphaned workload:
inventory-worker

Reason:
No matching Software Catalog entity.
```

### Acceptance Criteria

* [ ] Workload is discovered.
* [ ] Missing catalog entity is identified.
* [ ] Orphan is reported.
* [ ] Existing catalog entities are not affected.

---

# Scenario 9 – Detect a Stale Catalog Entity

## Objective

Demonstrate that the platform can identify potentially abandoned services.

### Action

Create or select a service whose metadata has not been updated within the configured freshness threshold.

### Expected Result

The catalog health report identifies the service as stale.

Example:

```text
Stale entity:
legacy-reporting-service

Last update:
> 90 days ago
```

### Acceptance Criteria

* [ ] Stale entity is detected.
* [ ] Last-known activity is reported.
* [ ] Service owner is identified.
* [ ] Stale entity is not automatically deleted.

---

# Scenario 10 – Generate Catalog Accuracy Report

## Objective

Demonstrate that Platform Engineering can measure catalog health.

### Action

Execute:

```bash
./scripts/catalog-accuracy-report.sh
```

### Expected Output

Example:

```text
Fortress Catalog Accuracy Report
================================

Total production services:       152
Cataloged services:              150
Catalog coverage:              98.68%

Services with owners:            150
Ownership coverage:            100.00%

Services with documentation:     146
Documentation coverage:         97.33%

Stale entities:                    2
Orphaned workloads:                1

Overall catalog health:          HEALTHY
```

### Acceptance Criteria

* [ ] Report executes successfully.
* [ ] Coverage is calculated.
* [ ] Ownership coverage is calculated.
* [ ] Documentation coverage is calculated.
* [ ] Stale entities are reported.
* [ ] Orphaned workloads are reported.
* [ ] Overall health status is produced.

---

# Scenario 11 – Simulate a Git Integration Failure

## Objective

Demonstrate that temporary upstream failures do not corrupt the catalog.

### Action

Temporarily make the Git integration unavailable.

Trigger a synchronization cycle.

### Expected Result

The synchronization job reports an error.

However, existing catalog entities remain available.

Example:

```text
Synchronization failed:
Git provider unavailable.

Catalog state:
PRESERVED

Next action:
Retry synchronization.
```

### Acceptance Criteria

* [ ] Failure is detected.
* [ ] Failure is logged.
* [ ] Existing catalog data remains available.
* [ ] Synchronization retries.
* [ ] Platform Engineering receives an actionable alert.

---

# Scenario 12 – Recover from Integration Failure

## Objective

Demonstrate automatic recovery.

### Action

Restore Git connectivity.

Trigger or wait for the next synchronization cycle.

### Expected Result

Synchronization succeeds.

```text
Synchronization successful.

Entities processed: 152
Entities updated: 3
Entities unchanged: 149
Errors: 0
```

### Acceptance Criteria

* [ ] Synchronization resumes.
* [ ] Catalog converges with source metadata.
* [ ] No duplicate entities are created.
* [ ] No manual catalog reconstruction is required.

---

# End-to-End Developer Journey

The complete happy path should be demonstrable as a single workflow.

```text
Developer
    │
    │ Discovers service
    ▼
Software Catalog
    │
    │ Finds owner
    ▼
Engineering Team
    │
    │ Finds repository
    ▼
Git
    │
    │ Updates metadata
    ▼
Pull Request
    │
    │ Validation
    ▼
CI Pipeline
    │
    │ Merge
    ▼
Catalog Synchronization
    │
    ▼
Software Catalog
    │
    ├── Documentation
    ├── Kubernetes
    ├── Monitoring
    └── Ownership
```

This demonstrates the intended operating model:

> **Metadata follows the software lifecycle instead of becoming a separate administrative process.**

---

# Failure Demonstration Matrix

The demonstration should explicitly test failure conditions.

| Failure                 | Expected Behavior          |
| ----------------------- | -------------------------- |
| Unknown owner           | Validation fails           |
| Duplicate entity        | Validation fails           |
| Missing required field  | Validation fails           |
| Git unavailable         | Existing catalog preserved |
| Kubernetes unavailable  | Existing catalog preserved |
| Orphaned workload       | Reported                   |
| Stale entity            | Reported                   |
| Synchronization failure | Retried and alerted        |
| Invalid lifecycle       | Validation fails           |

---

# Acceptance Test Summary

Initiative 1 passes acceptance when all critical scenarios succeed.

| Scenario                     | Result |
| ---------------------------- | ------ |
| Service discovery            | ☐      |
| Ownership discovery          | ☐      |
| Documentation discovery      | ☐      |
| Kubernetes discovery         | ☐      |
| Service registration         | ☐      |
| Invalid metadata rejection   | ☐      |
| Duplicate detection          | ☐      |
| Orphan detection             | ☐      |
| Stale entity detection       | ☐      |
| Accuracy reporting           | ☐      |
| Integration failure handling | ☐      |
| Recovery                     | ☐      |

All critical scenarios must pass before Initiative 1 is considered production-ready.

---

# Evidence Collection

The final implementation should preserve evidence of the demonstration.

Recommended evidence:

```text
assets/
├── backstage-service-page.png
├── catalog-search.png
├── ownership-view.png
├── kubernetes-view.png
├── validation-failure.png
├── duplicate-detection.png
├── orphan-detection.png
├── stale-entity-report.png
└── catalog-accuracy-report.txt
```

Evidence should demonstrate the actual Fortress implementation rather than screenshots of unrelated Backstage examples.

---

# Production Readiness Gate

The demonstration is not considered successful merely because the happy path works.

Before production adoption, Platform Engineering must confirm:

* [ ] Happy-path workflows work.
* [ ] Failure scenarios behave safely.
* [ ] Recovery has been tested.
* [ ] Catalog data survives application restart.
* [ ] Database recovery has been tested.
* [ ] Synchronization is observable.
* [ ] Validation policies are enforced.
* [ ] Runbooks exist.
* [ ] Ownership is assigned.
* [ ] Success metrics are measurable.

---

# Definition of Demonstrated Value

Initiative 1 demonstrates real platform value when a developer can answer:

> **"Who owns this service, where does it run, where is its code, and where do I find its operational information?"**

without asking Platform Engineering.

It demonstrates additional operational value when Platform Engineering can answer:

> **"Which services are unknown, unowned, stale, or incorrectly represented?"**

without manually inspecting repositories and Kubernetes clusters.

These two capabilities establish the fundamental value proposition of **Know Your Platform**:

**developers gain discoverability, while Platform Engineering gains operational visibility.**

---

# Transition to Success Metrics

The demonstration establishes that the platform works technically.

The next document measures whether it is delivering the intended organizational and operational outcomes.

`07-success-metrics.md` will therefore define the quantitative measurements used to determine whether Initiative 1 has actually improved Acme Corp's platform—not merely whether the software was successfully deployed.
