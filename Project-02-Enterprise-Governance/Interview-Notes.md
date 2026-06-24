# Interview Notes

---

## What is Unity Catalog?

Unity Catalog is Databricks' centralized governance layer that provides metadata management, permissions, lineage, auditing, discovery, and a unified namespace across multiple workspaces.

---

## What is a Metastore?

A Metastore is the centralized repository that stores governance metadata such as catalogs, schemas, tables, permissions, ownership, lineage, and storage mappings.

---

## Why do we need Unity Catalog if ADLS already exists?

ADLS stores data.

Unity Catalog governs data.

Unity Catalog provides:

- Permissions
- Lineage
- Auditing
- Discovery
- Ownership
- Multi-workspace governance

---

## What problem do Storage Credentials solve?

Storage Credentials solve the authentication problem between Databricks and cloud storage.

Instead of embedding secrets inside notebooks, Databricks authenticates through Managed Identities or Service Principals.

---

## What problem do External Locations solve?

External Locations provide governed mappings between Unity Catalog and cloud storage paths.

They allow administrators to control access through Unity Catalog rather than direct storage paths.

---

## Why Catalog First Architecture?

Users should interact with:

retailcorp.bronze.customers

instead of:

abfss://bronze@storageaccount...

This creates abstraction and reduces coupling to storage implementation.

---

## What is the difference between ADLS, Unity Catalog and Metastore?

ADLS

- Stores Data

Unity Catalog

- Governs Data

Metastore

- Stores Governance Metadata

---

## Why separate containers for Bronze, Silver and Gold?

Benefits:

- Independent lifecycle policies
- Security boundaries
- Better governance
- Cleaner ownership

---

## What is the principle behind Metastore design?

One Metastore Per Governance Boundary.

A single enterprise commonly uses one Metastore shared across Dev, Test, and Prod workspaces.
