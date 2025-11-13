# Accepted RFCs

> **Archive of approved Standard Change Proposals**

---

## Overview

This directory contains RFCs that have been:
1. Proposed as issues in this repository
2. Discussed by the community (minimum 14 days)
3. Voted on by the TSC
4. Approved (simple majority or higher)

---

## Naming Convention

RFCs are numbered sequentially:

```
0001-descriptive-name.md
0002-another-feature.md
...
```

**Format**: `NNNN-kebab-case-title.md`

---

## RFC Index

_No RFCs accepted yet - pending TSC formation._

| Number | Title | Author | Status | Implemented |
|--------|-------|--------|--------|-------------|
| - | - | - | - | - |

---

## Lifecycle

Once an RFC is accepted:

1. **Archived Here**: Full RFC text copied from issue to this directory
2. **Implementation Authorized**: PR can be opened to specification
3. **Status Tracked**: RFC marked as `implemented` when merged
4. **Immutable**: Accepted RFCs are never modified (amendments require new RFC)

---

## Searching

To find specific RFCs:

```bash
# Search by keyword
grep -r "keyword" accepted/

# List all RFCs
ls -1 accepted/*.md

# View RFC metadata
head -20 accepted/0001-*.md
```

---

## Historical Value

This archive serves as:
- **Specification rationale**: Why decisions were made
- **Community consensus record**: Who supported what
- **Design evolution**: How WEKAOU evolved over time
- **Learning resource**: Examples of good proposals

---

**Browse**: [All Accepted RFCs](https://github.com/zaste/wekaou-rfc/tree/main/accepted)  
**Propose**: [New RFC](https://github.com/zaste/wekaou-rfc/issues/new/choose)  
