# WEKAOU RFC Process

> **🗳️ The Parliamentary Process for WEKAOU Governance**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

---

## 📋 Purpose

This repository hosts the **Request for Comments (RFC) process** for proposing, discussing, and approving changes to the WEKAOU® standard.

**Critical Principle**: ALL changes to [wekaou-specification](https://github.com/zaste/wekaou-specification) MUST go through this RFC process. Direct PRs to the specification will be rejected.

---

## 🎯 What Requires an RFC?

### ✅ Requires RFC (Use This Process)

- Changes to META-2.5 Core (SPOC-M, CRL, K-Cycle)
- New patterns in META-2 Applied
- Promotion/demotion between tiers
- Governance changes (Charter, TSC mandate, etc.)
- Breaking changes to any specification
- New Working Group proposals

### ❌ Does NOT Require RFC

- Typo fixes and editorial clarifications
- Tooling improvements (compliance-suite, kos-ce)
- Community content (awesome-wekaou)
- Documentation improvements (if no spec changes)
- Tier-3 experimental contributions (lightweight PR review)

**When in doubt, ask in [wekaou-community](https://github.com/zaste/wekaou-community/discussions).**

---

## 🔄 The RFC Lifecycle

```
┌─────────────┐
│  PROPOSED   │  ← Issue opened with SCP template
└──────┬──────┘
       │
       ↓
┌─────────────┐
│ DISCUSSION  │  ← Community debates (min 14 days)
└──────┬──────┘
       │
       ↓
┌─────────────┐
│   VOTING    │  ← TSC votes (simple majority)
└──────┬──────┘
       │
   ┌───┴───┐
   ↓       ↓
┌────┐  ┌────┐
│ACCP│  │REJ │
│TED │  │ECTD│
└─┬──┘  └────┘
  │
  ↓
┌─────────────┐
│IMPLEMENTED  │  ← PR merged to specification
└─────────────┘
```

---

## 🚀 How to Submit an RFC

### Step 1: Check Existing RFCs

Search [issues](https://github.com/zaste/wekaou-rfc/issues) to avoid duplicates.

### Step 2: Open an Issue

Use the appropriate template:
- **Standard Change Proposal (SCP)**: For spec changes
- **Discussion**: For exploratory ideas
- **Governance Amendment**: For governance changes

### Step 3: Community Discussion

**Minimum Period**: 14 days  
**Goal**: Refine the proposal, surface concerns, build consensus

**Your Responsibilities**:
- Respond to questions and feedback
- Revise proposal based on input
- Document alternatives considered
- Engage constructively

### Step 4: TSC Review

Once discussion matures, a TSC member will:
1. Add label `status: voting`
2. Announce voting period (typically 7 days)
3. TSC members cast votes (approve/reject/abstain)
4. Results posted publicly

**Quorum**: 60% of TSC must participate  
**Approval**: Simple majority of votes cast  

### Step 5: Implementation

If accepted:
1. RFC moved to `/accepted/` directory
2. Implementation PR can be opened in specification repo
3. PR must reference the accepted RFC number
4. Merge guard workflows verify linkage

---

## 📝 RFC States

| State | Label | Meaning |
|-------|-------|----------|
| **Proposed** | `status: proposed` | Initial submission |
| **Under Discussion** | `status: discussion` | Active community debate |
| **Voting** | `status: voting` | TSC voting in progress |
| **Accepted** | `status: accepted` | Approved for implementation |
| **Rejected** | `status: rejected` | Not approved (with rationale) |
| **Withdrawn** | `status: withdrawn` | Author withdrew proposal |
| **Implemented** | `status: implemented` | Merged to specification |

---

## 📂 Repository Structure

```
rfc/
├── README.md                    # This file
├── LICENSE                      # CC BY 4.0
│
├── /.github/
│   └── ISSUE_TEMPLATE/
│       ├── scp-proposal.yml     # Standard Change Proposal
│       ├── discussion.yml       # Exploratory discussion
│       └── governance.yml       # Governance amendments
│
├── /accepted/                   # Archive of approved RFCs
│   ├── 0001-example-rfc.md
│   └── README.md
│
├── /templates/                  # Markdown templates
│   ├── scp-template.md
│   └── governance-template.md
│
└── /resources/                  # Supporting materials
    ├── voting-guidelines.md
    └── writing-rfcs.md
```

---

## ✍️ Writing a Good RFC

### Essential Elements

1. **Summary**: One-paragraph overview
2. **Motivation**: Why is this change needed?
3. **Detailed Design**: How will it work?
4. **Alternatives**: What other options were considered?
5. **Impact**: Who/what is affected?
6. **Migration**: How do existing implementations adapt?

### Tips

- **Be specific**: Vague proposals are hard to evaluate
- **Show examples**: Code/pseudocode helps clarify
- **Acknowledge trade-offs**: Every design has pros/cons
- **Link to prior art**: Reference similar work
- **Engage early**: Share draft in Discussions first

---

## 🗳️ Voting (TSC Members Only)

### Voting Process

1. TSC member adds `status: voting` label
2. Voting period begins (announced in issue)
3. Each TSC member comments: `+1` (approve), `-1` (reject), `0` (abstain)
4. After voting period, results tallied
5. Outcome announced with rationale

### Voting Power

- **Simple Majority**: Most changes (50% + 1 of votes cast)
- **Supermajority**: Tier 2→1 promotions, governance (2/3 of votes cast)
- **Unanimous**: Charter amendments (100% of votes cast)

### Transparency

- All votes are public
- Rationale for rejection must be provided
- Voting history preserved in issue timeline

---

## 📚 Resources

- [How to Write a Good RFC](./resources/writing-rfcs.md)
- [Voting Guidelines for TSC](./resources/voting-guidelines.md)
- [RFC Process FAQ](./resources/faq.md)
- [Governance Charter](https://github.com/zaste/wekaou-governance/blob/main/CHARTER.md)

---

## 🔗 Related Repositories

- [wekaou-specification](https://github.com/zaste/wekaou-specification) - The canonical standard
- [wekaou-governance](https://github.com/zaste/wekaou-governance) - ACA charter and policies
- [wekaou-community](https://github.com/zaste/wekaou-community) - Public discussions

---

## 🤝 Code of Conduct

All participants must adhere to the [WEKAOU Code of Conduct](https://github.com/zaste/wekaou-.github/blob/main/CODE_OF_CONDUCT.md).

**Key Principles**:
- Assume good faith
- Focus on ideas, not people
- Be respectful of diverse perspectives
- Constructive criticism, not attacks

---

## 📊 Current Status

**TSC Formed**: No (pending inaugural ACA assembly)  
**RFCs Submitted**: 0  
**RFCs Accepted**: 0  
**Process Status**: Pre-governance (informal discussion)

**Note**: Until TSC is formed, this process is informal. Early proposals help shape the specification but formal voting awaits governance structure.

---

## 💡 Examples

Once RFCs start flowing, we'll showcase exemplary proposals here.

---

## ❓ Questions?

- **Process questions**: Ask in [wekaou-community](https://github.com/zaste/wekaou-community/discussions)
- **Technical questions**: Reference [wekaou-specification](https://github.com/zaste/wekaou-specification)
- **Governance questions**: See [wekaou-governance](https://github.com/zaste/wekaou-governance)

---

<div align="center">

**Democratic governance for a coherent standard.**

[Submit RFC](https://github.com/zaste/wekaou-rfc/issues/new/choose) • [View Accepted RFCs](./accepted/) • [Join Community](https://github.com/zaste/wekaou-community)

</div>
