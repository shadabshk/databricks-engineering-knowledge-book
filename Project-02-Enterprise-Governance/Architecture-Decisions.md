# Architecture Decisions

---

## Decision #1

### Topic

Workspace Strategy

### Alternatives Considered

- Single Workspace
- Dev + Test + Prod

### Final Decision

Logical:

- Dev
- Test
- Prod

Physical:

- Dev Only

### Reason

Provides enterprise architecture understanding without unnecessary cost.

---

## Decision #2

### Topic

Storage Strategy

### Alternatives Considered

- Single Storage Account
- Multiple Storage Accounts

### Final Decision

Single Storage Account

stretailcorpdev001

### Reason

Focus on governance and Unity Catalog concepts.

---

## Decision #3

### Topic

Catalog First Architecture

### Alternatives Considered

- Storage First
- Catalog First

### Final Decision

Catalog First

### Reason

Users should think in terms of business entities instead of storage paths.

---

## Decision #4

### Topic

Medallion Storage Layout

### Alternatives Considered

- Single Container with Folders
- Separate Containers

### Final Decision

Separate Containers

landing
bronze
silver
gold

### Reason

Better governance and lifecycle management.

---

## Decision #5

### Topic

Metastore Strategy

### Alternatives Considered

- One Metastore
- Multiple Metastores

### Final Decision

One Metastore

### Reason

Centralized governance and consistent metadata management.
