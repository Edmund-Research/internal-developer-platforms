# 07 – Success Metrics

> **Project Fortress**
> **Initiative 1 – Know Your Platform**

---

# Purpose

This document defines how Acme Corp will measure the success of Initiative 1: **Know Your Platform**.

The objective is to establish measurable evidence that the Software Catalog improves service discoverability, metadata quality, operational visibility, and developer experience.

Success will not be determined solely by whether Backstage is deployed or whether services appear in the catalog.

The initiative is successful only when the catalog becomes a **trusted and actively used platform capability**.

---

# Measurement Philosophy

Fortress follows four measurement principles.

## Measure Outcomes, Not Activity

The number of catalog entities created is useful, but it does not prove that the platform is valuable.

We therefore measure outcomes such as:

* discoverability
* ownership coverage
* metadata accuracy
* operational readiness
* developer effort
* platform reliability

---

## Establish a Baseline Before Optimization

The current-state assessment established the initial baseline.

Future measurements will be compared against that baseline rather than against arbitrary targets alone.

---

## Measure Both Platform Health and User Value

Two categories of metrics are required:

```text
                    Fortress Metrics
                          │
              ┌───────────┴───────────┐
              │                       │
              ▼                       ▼
       Platform Health          Developer Value
              │                       │
              ▼                       ▼
      Is it working?           Is it useful?
```

A technically healthy catalog that nobody trusts or uses is not a successful Internal Developer Platform.

---

## Failure Signals Are First-Class Metrics

The platform must measure failure conditions rather than hiding them.

Examples include:

* orphaned workloads
* stale entities
* synchronization failures
* invalid metadata
* missing ownership
* broken documentation links

These are not merely implementation defects.

They are signals about the health of the platform ecosystem.

---

# Metric Categories

Initiative 1 uses six primary metric categories:

1. Catalog Coverage
2. Metadata Quality
3. Synchronization Health
4. Operational Visibility
5. Developer Experience
6. Platform Reliability

---

# 1. Catalog Coverage

## Catalog Coverage

Measures the percentage of known production services represented in the Software Catalog.

### Formula

```text
Catalog Coverage =
Cataloged Production Services
-------------------------------- × 100
Total Known Production Services
```

### Baseline

**0%**

### Target

**≥98%**

### Stretch Target

**100%**

### Measurement Frequency

Daily.

### Source

* Software Catalog
* Kubernetes inventory
* service inventory

---

# 2. Ownership Coverage

Measures the percentage of production services with a valid accountable owner.

### Formula

```text
Ownership Coverage =
Services With Valid Owners
--------------------------- × 100
Cataloged Production Services
```

### Baseline

Unknown.

### Target

**100%**

### Why It Matters

Ownership is one of the most important pieces of operational metadata.

A service without an accountable owner represents an unresolved operational risk.

---

# 3. Repository Coverage

Measures how many cataloged services have a valid source repository reference.

### Target

**100%**

### Validation

The platform should verify that:

* repository exists
* repository reference is valid
* repository remains accessible
* service metadata points to the expected location

---

# 4. Documentation Coverage

Measures the percentage of production services with required operational documentation.

### Target

**≥95%**

Required documentation may include:

* README
* operational runbook
* architecture documentation
* API documentation where applicable

Documentation coverage should not be interpreted as proof of documentation quality.

That distinction will be addressed in later Fortress initiatives.

---

# 5. Metadata Quality

## Valid Entity Rate

Measures the percentage of catalog entities that pass all validation rules.

### Formula

```text
Valid Entity Rate =
Valid Catalog Entities
----------------------- × 100
Total Catalog Entities
```

### Target

**≥99%**

---

## Missing Metadata Rate

Measures the percentage of entities missing required metadata.

### Target

**<1%**

Required fields include:

* owner
* lifecycle
* repository
* description
* service type

---

# 6. Metadata Freshness

Measures how recently catalog entities have been updated or verified.

### Target

**≥98% of production entities within freshness threshold**

The exact threshold will depend on service type and lifecycle.

For example:

| Service Type       | Freshness Threshold |
| ------------------ | ------------------- |
| Production         | 30 days             |
| Active development | 60 days             |
| Deprecated         | 90 days             |

The threshold measures metadata health, not application activity.

---

# 7. Orphaned Workloads

Measures Kubernetes workloads that cannot be associated with a known catalog entity.

### Formula

```text
Orphan Rate =
Unmatched Production Workloads
-------------------------------- × 100
Total Production Workloads
```

### Target

**<1%**

### Desired State

Ideally:

**0 orphaned production workloads**

---

# 8. Stale Entities

Measures catalog entities that exceed the defined freshness threshold.

### Target

**<2%**

Stale entities should trigger investigation rather than automatic deletion.

A stale entity may indicate:

* abandoned software
* missing ownership
* incomplete migration
* documentation neglect
* synchronization failure

---

# 9. Synchronization Health

The catalog must continuously synchronize with upstream systems.

## Synchronization Success Rate

### Formula

```text
Successful Syncs
---------------- × 100
Total Sync Attempts
```

### Target

**≥99%**

---

## Synchronization Recovery Time

Measures the time required for synchronization to recover after a failure.

### Target

**<15 minutes**

---

## Synchronization Error Rate

### Target

**<1%**

Errors must be classified so that recurring failures can be distinguished from transient infrastructure failures.

---

# 10. Data Convergence

The catalog should converge toward the state represented by its authoritative metadata sources.

## Convergence Time

Measures how long it takes for an approved metadata change to become visible in the catalog.

### Target

**<5 minutes**

Example:

```text
Git Merge
   │
   ▼
Synchronization
   │
   ▼
Catalog Updated

Target: <5 minutes
```

This metric becomes particularly important once Fortress begins integrating catalog metadata into automated platform workflows.

---

# 11. Developer Experience

Technical health alone is insufficient.

Fortress must measure whether developers can actually use the catalog.

---

## Service Discovery Time

Measures the time required for a developer to locate basic information about an unfamiliar service.

The target journey is:

```text
Search service
     ↓
Identify owner
     ↓
Find repository
     ↓
Find documentation
     ↓
Find operational resources
```

### Baseline

To be established during the pilot.

### Target

**≤2 minutes**

---

# 12. Platform Support Deflection

Measures platform requests that developers can resolve using the Software Catalog without contacting Platform Engineering.

Examples:

* "Who owns this service?"
* "Where is this repository?"
* "Where is the runbook?"
* "Where does this service run?"

### Target

Establish baseline during Phase 1.

Then achieve:

**≥50% reduction in catalog-related informational requests.**

---

# 13. Onboarding Effort

Measures Platform Engineering effort required to register a service.

### Baseline

Manual.

### Target

After organization-wide rollout:

**No routine manual catalog registration.**

A developer should be able to register a service through the standard workflow without Platform Engineering editing catalog metadata on their behalf.

---

# 14. Platform Reliability

The Software Catalog itself becomes a production dependency.

It therefore requires reliability measurements.

## Catalog Availability

### Target

**≥99.9%**

---

## Catalog API Latency

For normal catalog queries:

### Target

**p95 <500 ms**

---

## Failed Catalog Requests

### Target

**<1%**

---

# 15. Incident Response Value

The catalog should measurably improve operational discovery during incidents.

## Ownership Discovery Time

Measures the time required for an incident responder to identify the responsible team.

### Baseline

To be established through incident simulations.

### Target

**≤30 seconds**

---

## Operational Resource Discovery

Measures the time required to locate:

* dashboard
* runbook
* repository
* service owner

### Target

**≤2 minutes**

---

# 16. Composite Catalog Health Score

Platform Engineering should expose a single high-level indicator while retaining the underlying metrics.

A proposed composite score:

```text
Catalog Health Score

30%  Coverage
20%  Ownership
15%  Metadata Quality
15%  Synchronization Health
10%  Freshness
10%  Orphan Rate
```

The score should never replace the underlying metrics.

Its purpose is to provide leadership and Platform Engineering with a high-level signal.

---

# Target Score

The initial production target is:

**≥95 / 100**

However, individual critical metrics must still meet their own thresholds.

A high composite score must not conceal a serious failure such as:

```text
Catalog Health Score: 96

Ownership Coverage: 72%
```

Critical dimensions should therefore have explicit minimum thresholds.

---

# Metrics Dashboard

The implementation should provide a catalog health dashboard containing at minimum:

```text
+------------------------------------------------------+
|             FORTRESS CATALOG HEALTH                  |
+------------------------------------------------------+
|                                                      |
| Catalog Coverage             98.7%       HEALTHY     |
| Ownership Coverage           100%        HEALTHY     |
| Documentation Coverage       97.3%       HEALTHY     |
| Valid Entity Rate            99.4%       HEALTHY     |
| Synchronization Success      99.8%       HEALTHY     |
| Stale Entities               1.3%        HEALTHY     |
| Orphaned Workloads           0.6%        WARNING     |
|                                                      |
+------------------------------------------------------+
| Catalog Availability         99.96%                  |
| Sync Recovery                8m                      |
+------------------------------------------------------+
```

The dashboard becomes an operational interface rather than a reporting artifact.

---

# Measurement Sources

Metrics should be derived from authoritative systems wherever possible.

| Metric                   | Primary Source            |
| ------------------------ | ------------------------- |
| Catalog Coverage         | Backstage + Kubernetes    |
| Ownership                | Backstage                 |
| Repository Coverage      | Git + Backstage           |
| Documentation Coverage   | Backstage                 |
| Metadata Quality         | Validation pipeline       |
| Freshness                | Catalog metadata          |
| Orphan Rate              | Kubernetes + Catalog      |
| Sync Success             | Synchronization jobs      |
| Catalog Availability     | Platform monitoring       |
| API Latency              | Platform telemetry        |
| Developer Discovery Time | User research / telemetry |
| Support Deflection       | Platform ticket data      |

---

# Alerting Thresholds

Not every metric requires an alert.

Alerts should focus on conditions requiring operator action.

| Condition                   | Severity |
| --------------------------- | -------- |
| Catalog unavailable         | Critical |
| Sync failure >15 minutes    | High     |
| Ownership coverage <98%     | High     |
| Catalog coverage <95%       | High     |
| Orphan rate >2%             | Medium   |
| Stale entities >5%          | Medium   |
| Documentation coverage <90% | Low      |

This prevents alert fatigue while ensuring meaningful degradation is visible.

---

# Measurement Cadence

## Real-Time

Monitor continuously:

* availability
* API latency
* synchronization failures

---

## Daily

Calculate:

* catalog coverage
* ownership coverage
* stale entities
* orphaned workloads
* metadata quality

---

## Weekly

Review:

* onboarding volume
* support deflection
* metadata trends
* recurring synchronization failures

---

## Monthly

Review with Platform Engineering leadership:

* overall catalog health
* adoption trends
* operational incidents
* developer experience
* progress toward targets

---

# Baseline vs Target

The transformation can now be represented quantitatively.

| Metric                 | Baseline     | Target             |
| ---------------------- | ------------ | ------------------ |
| Catalog Coverage       | 0%           | ≥98%               |
| Ownership Coverage     | Unknown      | 100%               |
| Repository Coverage    | Unknown      | 100%               |
| Documentation Coverage | Unknown      | ≥95%               |
| Valid Entity Rate      | N/A          | ≥99%               |
| Metadata Freshness     | Not measured | ≥98%               |
| Orphan Rate            | Not measured | <1%                |
| Stale Entities         | Not measured | <2%                |
| Sync Success           | N/A          | ≥99%               |
| Catalog Availability   | N/A          | ≥99.9%             |
| Discovery Time         | Not measured | ≤2 min             |
| Ownership Discovery    | Not measured | ≤30 sec            |
| Manual Registration    | High         | 0 routine requests |

This table provides the measurable transformation baseline for Initiative 1.

---

# Anti-Metrics

Fortress will deliberately avoid using certain measurements as primary indicators of success.

## Number of Catalog Entities

A large catalog does not necessarily mean a useful catalog.

---

## Backstage Page Views

Traffic can indicate adoption but does not prove value.

---

## Number of Plugins Installed

Technical complexity is not a success metric.

---

## Number of Metadata Fields

More metadata does not automatically mean better metadata.

---

# Measurement Risks

## Metric Gaming

Teams may create superficial metadata to satisfy coverage targets.

**Mitigation:** Validate metadata against authoritative systems.

---

## False Accuracy

A catalog entity may technically exist while containing incorrect information.

**Mitigation:** Measure freshness, repository validity, ownership validity, and workload correlation.

---

## Over-Alerting

Excessive alerts may cause platform engineers to ignore legitimate issues.

**Mitigation:** Alert only on actionable thresholds.

---

## Adoption Without Value

Developers may use the portal because they are required to, without benefiting from it.

**Mitigation:** Measure discovery time and support deflection alongside usage.

---

# Definition of Success

Initiative 1 is successful when Acme Corp can demonstrate all of the following:

### Visibility

At least **98% of production services** are represented in the Software Catalog.

### Accountability

**100% of production services** have verified ownership.

### Accuracy

At least **99% of catalog entities** pass metadata validation.

### Synchronization

At least **99% of synchronization operations** complete successfully.

### Reliability

The catalog achieves **≥99.9% availability**.

### Operational Discovery

Engineers can identify service ownership within **30 seconds** and locate core operational information within **2 minutes**.

### Automation

Routine catalog registration no longer requires Platform Engineering intervention.

### Continuous Health

Orphaned, stale, and invalid entities are automatically detected rather than discovered manually.

---

# Measurement Ownership

Platform Engineering owns the measurement system.

However, the data represents shared engineering responsibility.

| Responsibility         | Owner                                |
| ---------------------- | ------------------------------------ |
| Platform availability  | Platform Engineering                 |
| Catalog infrastructure | Platform Engineering                 |
| Synchronization        | Platform Engineering                 |
| Metadata accuracy      | Service Teams                        |
| Ownership accuracy     | Service Teams                        |
| Documentation quality  | Service Teams                        |
| Catalog standards      | Platform Engineering                 |
| Developer experience   | Platform Engineering + Service Teams |

This distinction is important:

> **Platform Engineering owns the platform; engineering teams own the accuracy of their services.**

---

# Long-Term Measurement

The metrics introduced here become inputs to later Fortress initiatives.

For example:

* Catalog coverage feeds platform adoption metrics.
* Ownership metadata supports SLO ownership.
* Service relationships support dependency mapping.
* Catalog health feeds platform reliability.
* Service metadata enables cost attribution.
* Developer discovery metrics inform developer experience improvements.

The Software Catalog therefore becomes both a platform capability and a source of operational telemetry.

---

# Success Gate

Initiative 1 may proceed to its final retrospective only after:

* [ ] Coverage targets are achieved.
* [ ] Ownership targets are achieved.
* [ ] Metadata validation is operational.
* [ ] Synchronization reliability targets are achieved.
* [ ] Catalog availability target is achieved.
* [ ] Failure conditions are observable.
* [ ] Developer discovery workflow has been measured.
* [ ] Catalog health dashboard is operational.
* [ ] Baseline-to-target measurements are documented.

---

# Transition to Lessons Learned

The metrics establish whether Initiative 1 succeeded.

The final document, `08-lessons-learned.md`, will capture what the Platform Engineering team learned while designing, implementing, operating, and rolling out the Software Catalog.

It will distinguish between:

* technical lessons
* architectural lessons
* operational lessons
* developer experience lessons
* organizational lessons

These findings will become explicit inputs into **Initiative 2 – Golden Paths**, ensuring that Fortress evolves based on evidence rather than assumptions.
