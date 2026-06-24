# Project 02 - Enterprise Data Lake & Governance Platform

# DIVE Knowledge Book

---

# Concept: Environment Strategy (Dev / Test / Prod)

## Question

Should we create:

- One Workspace
- Dev + Test + Prod

## My Initial Answer

Dev + Test + Prod

## What I Missed

Architecture is not about creating more resources. It is about balancing:

- Cost
- Risk
- Complexity
- Learning Value

## Deep Explanation

In enterprise environments:

Dev → Test → Prod

Each environment serves a different purpose.

### Dev

- Development
- Experimentation
- Notebook creation

### Test

- Integration testing
- Validation
- User acceptance testing

### Prod

- Business-critical workloads
- Reporting
- Analytics

For this project:

Logical Design:

Dev + Test + Prod

Physical Implementation:

Dev Only

## Interview Answer

In enterprise environments I recommend separate Dev, Test, and Prod workspaces. For learning projects I often implement only Dev while documenting the promotion path to Test and Prod.

## Lessons Learned

Environment separation is a risk management strategy.

---

# Concept: Storage Strategy

## Question

One Storage Account or Multiple Storage Accounts?

## My Initial Answer

One Storage Account

## Deep Explanation

Multiple storage accounts introduce:

- Networking complexity
- RBAC complexity
- Lifecycle complexity

Since our objective is governance and Unity Catalog, a single storage account allows us to focus on core concepts.

Final Decision:

stretailcorpdev001

## Interview Answer

For learning and proof-of-concept environments, I prefer a single storage account. For large enterprises, multiple storage accounts may be introduced for compliance, networking, or business-unit isolation.

## Lessons Learned

Reduce variables while learning.

---

# Concept: Catalog First Architecture

## Question

Should users think in terms of storage paths or catalogs?

## My Initial Answer

Catalog First

## Deep Explanation

Without Unity Catalog:

Users access:

abfss://bronze@storageaccount...

With Unity Catalog:

SELECT * FROM retailcorp.bronze.customers

Users interact with business entities.

Storage implementation becomes an internal concern.

Logical Layer:

retailcorp.bronze.customers

Physical Layer:

ADLS → Container → Folder

## Interview Answer

Unity Catalog provides a logical abstraction layer that allows users to access data through business-friendly names instead of storage paths.

## Lessons Learned

Abstraction reduces coupling.

---

# Concept: Containers vs Folders

## Question

Should Medallion Architecture use:

- Separate Containers
OR
- One Container with Folders

## My Initial Answer

One Container with Folders

## What I Missed

Governance and lifecycle management.

## Deep Explanation

Separate containers provide:

- Security boundaries
- Independent retention policies
- Cleaner ownership
- Better governance

Final Decision:

landing
bronze
silver
gold

Containers

## Interview Answer

Separate containers provide stronger governance boundaries and simpler lifecycle management.

## Lessons Learned

Operational simplicity is not always the primary design objective.

---

# Concept: Why Unity Catalog Exists

## Question

Why do we need Unity Catalog if ADLS already stores data?

## My Initial Answer

Permissions and Lineage

## What I Missed

Unity Catalog also provides:

- Governance
- Metadata
- Auditing
- Discovery
- Ownership
- Multi-workspace management

## Deep Explanation

ADLS stores files.

Unity Catalog governs data assets.

Mental Model:

ADLS = Stores Data

Unity Catalog = Governs Data

## Interview Answer

Unity Catalog provides centralized governance, metadata management, lineage, auditing, permissions, and a unified namespace across multiple workspaces.

## Lessons Learned

Storage and governance are different responsibilities.

---

# Concept: Storage Credentials

## Question

Why not store storage account keys directly inside notebooks?

## My Initial Answer

Security

## What I Missed

Storage Credentials solve authentication architecture problems.

## Deep Explanation

Without Storage Credentials:

Secrets are embedded in notebooks.

With Storage Credentials:

Databricks
↓
Managed Identity
↓
ADLS

Authentication becomes centralized and secure.

## Interview Answer

Storage Credentials abstract cloud storage authentication and eliminate the need to embed secrets in notebooks.

## Lessons Learned

The primary problem is authentication, not permissions.

---

# Concept: External Locations

## Question

Why do External Locations exist?

## My Initial Answer

To restrict storage access.

## What I Missed

External Locations are governance objects.

## Deep Explanation

External Locations map:

Unity Catalog
↓
Approved Storage Path

Example:

bronze_loc
↓
abfss://bronze@storage...

This allows Unity Catalog to govern storage paths.

## Interview Answer

External Locations provide a governed mapping between Unity Catalog and cloud storage locations.

## Lessons Learned

External Locations are governance boundaries, not user folders.

---

# Concept: Metastore

## Question

What is a Metastore?

## My Initial Answer

A place where metadata is stored.

## What I Missed

A Metastore is the governance brain of Unity Catalog.

## Deep Explanation

A Metastore stores:

- Catalogs
- Schemas
- Tables
- Permissions
- Ownership
- Lineage
- Storage mappings

It does not store business data.

Mental Model:

ADLS = Stores Data

Unity Catalog = Governs Data

Metastore = Stores Governance Metadata

## Interview Answer

A Metastore is the centralized repository that stores governance metadata for Unity Catalog.

## Lessons Learned

Governance metadata is more important than the word metadata itself.

---

# Concept: One Metastore vs Multiple Metastores

## Question

Should Dev, Test, and Prod use one Metastore?

## My Initial Answer

One Metastore

## Deep Explanation

Principle:

One Metastore Per Governance Boundary

RetailCorp:

Dev
Test
Prod
↓
One Metastore

Benefits:

- Consistent permissions
- Consistent ownership
- Consistent lineage
- Consistent governance

## Interview Answer

Most organizations use one Metastore per governance boundary to provide centralized governance across multiple workspaces.

## Lessons Learned

The objective is governance consistency.
