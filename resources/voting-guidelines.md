# Voting Guidelines for TSC Members

> **How to evaluate and vote on RFCs**

---

## Your Responsibility

As a TSC member, your vote shapes the WEKAOU standard. Vote with:
- **Technical rigor**: Ensure quality and coherence
- **Community perspective**: Consider impact on implementers
- **Long-term thinking**: Avoid short-term hacks

---

## Evaluation Criteria

### 1. Technical Soundness

**Questions**:
- Is the design internally consistent?
- Does it interact correctly with existing features?
- Are edge cases handled?
- Is the specification unambiguous?

**Red Flags**:
- Vague semantics ("it should somehow...")
- Missing error handling
- Unclear interaction with existing spec

---

### 2. Necessity

**Questions**:
- Does this solve a real problem?
- Is the problem significant enough to warrant spec change?
- Can it be solved in userland (Tier-3) instead?

**Red Flags**:
- "Nice to have" without clear use case
- Solution in search of a problem
- Niche need affecting <5% of users

---

### 3. Scope Appropriateness

**Questions**:
- Is this the right level of abstraction for WEKAOU?
- Does it belong in Core vs Applied?
- Is it general enough or too domain-specific?

**Red Flags**:
- Domain-specific logic in META-2.5 Core
- General infrastructure in Tier-3
- Overengineering (YAGNI violations)

---

### 4. Backward Compatibility

**Questions**:
- Breaking change justified?
- Is migration path reasonable?
- Can we avoid breaking compatibility?

**Red Flags**:
- Unnecessary breaking change
- No migration strategy
- Short deprecation timeline

---

### 5. Implementation Burden

**Questions**:
- Can implementations reasonably support this?
- Is complexity proportional to value?
- Does it require ecosystem coordination?

**Red Flags**:
- Requires rewrite of major components
- Expensive for negligible benefit
- Impossible to implement in some languages

---

### 6. Community Consensus

**Questions**:
- What's the community sentiment?
- Are major implementers supportive?
- Were concerns addressed?

**Red Flags**:
- Major unresolved objections
- Key stakeholders opposed
- Author unresponsive to feedback

---

## Voting Process

### Step 1: Thorough Review

- **Read the RFC fully** (don't skim)
- **Read discussion comments** (context matters)
- **Test mental implementation** (can you code this?)
- **Consider alternatives** (are they truly inferior?)

### Step 2: Engage in Discussion

Before voting:
- Ask clarifying questions
- Raise concerns publicly
- Suggest improvements
- Give author time to respond

**Don't**: Vote immediately or stay silent until voting

### Step 3: Cast Your Vote

**Format**: Comment on the RFC issue

```markdown
## Vote: [+1 / -1 / 0]

### Rationale
[Your reasoning, especially if -1]

### Conditions (optional)
[If +1 conditional on changes]
```

**Vote Meanings**:
- **+1**: Approve (I support merging this)
- **-1**: Reject (I oppose merging this)
- **0**: Abstain (I have no strong opinion or conflict of interest)

### Step 4: Respect the Outcome

Once voting closes:
- Accept majority decision gracefully
- Support implementation even if you voted -1
- Maintain cohesion and professionalism

---

## Voting Scenarios

### Scenario 1: Clear Approve (+1)

```markdown
## Vote: +1

### Rationale
This RFC addresses a real pain point (confidence information loss)
with a clean, non-breaking design. The `mechanism.confidence` field
is semantically correct, has clear semantics, and minimal implementation
burden. Community feedback was positive and concerns were addressed.
```

### Scenario 2: Conditional Approve (+1 with conditions)

```markdown
## Vote: +1

### Rationale
Strong proposal, but needs minor changes before merging.

### Conditions
1. Add validation rule: confidence MUST be null or in [0.0, 1.0]
   (currently says "if present", but doesn't handle invalid values)
2. Clarify in spec: absence of field ≠ confidence=1.0

If author addresses these, my vote stands. If not, I'd reconsider.
```

### Scenario 3: Reject (-1)

```markdown
## Vote: -1

### Rationale
While I appreciate the motivation, I oppose this for two reasons:

1. **Premature**: We don't have enough real-world evidence that
   implementations need this. Only 1 known use case (ML predictions).
   Suggest: Let Tier-3 experiments prove the need first.

2. **Semantic ambiguity**: The spec says 0.0 = "certainty of negation"
   but SPOC-M triples are affirmations. What does it mean for
   `[X] has_property [Y]` to have confidence 0.0? That it DOESN'T
   have the property? Then why is the triple there?

### Alternative Path
I'd support a revised RFC that:
- Restricts range to (0.0, 1.0] (exclude 0.0)
- Gathers evidence from Tier-3 implementations first
```

### Scenario 4: Abstain (0)

```markdown
## Vote: 0 (Abstain)

### Rationale
I work for a company implementing confidence scoring, creating a
potential conflict of interest. Deferring to other TSC members.
```

---

## Special Cases

### Tie Votes

If votes are tied (e.g., 2-2 with 1 abstention):
- **TSC Chair casts tiebreaker vote**
- Chair should explain reasoning
- If Chair abstained/absent, RFC is rejected (status quo bias)

### Insufficient Quorum

If <60% of TSC votes:
- **Voting period extended 7 days**
- If still no quorum, RFC is deferred (not rejected)
- Chair may contact non-voting members

### Changed Circumstances

If significant new information emerges after voting:
- Any TSC member can call for **revote**
- Requires 2+ members to support revote
- Original votes are discarded

---

## Voting Ethics

### Do

- **Vote your conscience** (not politics)
- **Explain rejections** (help author improve)
- **Consider implementation diversity** (not just your use case)
- **Change your mind** (if discussion convinces you)

### Don't

- **Vote strategically** (e.g., reject to delay competitor)
- **Rubber-stamp** (always read thoroughly)
- **Hold grudges** (vote on merit, not history)
- **Demand perfection** (good enough often is)

---

## Accountability

Your votes are:
- **Public**: Recorded in issue timeline
- **Permanent**: Cannot be deleted/edited
- **Consequential**: You're responsible for spec quality

Vote as if the entire community is watching—because they are.

---

## Questions?

For voting process questions, contact other TSC members or raise in
TSC meetings.
