# How to Write a Good RFC

> **Practical guide for crafting effective Standard Change Proposals**

---

## The Golden Rule

**Clarity > Cleverness**

A good RFC is one that anyone can understand, evaluate, and implement without ambiguity.

---

## Anatomy of an Excellent RFC

### 1. Summary (The Hook)

**Goal**: Get reader interested in 30 seconds

**Formula**: [Action] [Target] to [Benefit]

**Example**:
> "This RFC proposes to add a `confidence` field to SPOC-M mechanism metadata to enable probabilistic reasoning in K-OS systems."

**Anti-patterns**:
- Too vague: "Improve SPOC-M"
- Too detailed: "Add mechanism.confidence field type float range 0-1 with..."

---

### 2. Motivation (The Why)

**Goal**: Convince reader this problem is worth solving

**Structure**:
1. **Current state**: What exists today
2. **Problem**: What's painful/missing/broken
3. **Impact**: Who suffers and how much

**Example**:
```markdown
## Motivation

### Current State
SPOC-M mechanism blocks capture provenance (source, derivation method)
but do not express certainty about the derived knowledge.

### Problem
K-OS systems often work with probabilistic or uncertain data:
- Sensor readings with measurement error
- ML model predictions with confidence scores
- Human annotations with inter-rater disagreement

Currently, implementers create ad-hoc fields like `_confidence`,
`certainty`, or `probability`, fragmenting the ecosystem.

### Impact
- Interoperability: Systems can't exchange uncertainty information
- Loss of information: Critical confidence data is dropped
- User confusion: No standard way to express "I'm 80% sure"
```

---

### 3. Detailed Design (The How)

**Goal**: Provide sufficient detail for implementation

**Include**:
- Exact schemas/grammar/state machines
- Examples (both simple and complex)
- Edge cases and error handling
- Interaction with existing features

**Example**:
```markdown
## Detailed Design

### Schema Change

Add optional `confidence` field to SPOC-M mechanism block:

```json
{
  "mechanism": {
    "source": "ml-model-v2",
    "derivation": "classification",
    "confidence": 0.87  // NEW: float in [0.0, 1.0]
  }
}
```

### Semantics

- **Type**: Float
- **Range**: [0.0, 1.0] inclusive
- **Interpretation**: 
  - 1.0 = Absolute certainty
  - 0.5 = Maximum uncertainty (coin flip)
  - 0.0 = Absolute certainty of negation
- **Optional**: If absent, no confidence information available
  (NOT equivalent to 0.0 or 1.0)

### Examples

#### High Confidence
```crl
[Patient:12345] has_diagnosis [Disease:Pneumonia]
  @mechanism {
    source: "radiologist-dr-smith",
    derivation: "x-ray-analysis",
    confidence: 0.95
  }
```

#### Low Confidence
```crl
[Stock:AAPL] will_trend [Direction:Up]
  @mechanism {
    source: "prediction-model",
    confidence: 0.52  // Barely better than chance
  }
```

### Validation Rules

1. If present, MUST be float
2. MUST be in range [0.0, 1.0]
3. OOS validation error if out of range
```

**Anti-patterns**:
- No examples
- Vague semantics ("add a confidence thing")
- Missing error cases

---

### 4. Alternatives (The Road Not Taken)

**Goal**: Show you've done your homework

**Structure**: For each alternative:
1. Describe it
2. Pros
3. Cons
4. Why rejected

**Example**:
```markdown
## Alternatives Considered

### Alternative 1: Separate Uncertainty Block

Add top-level `uncertainty` block:
```json
{
  "subject": ...,
  "predicate": ...,
  "object": ...,
  "uncertainty": {  // NEW
    "confidence": 0.87
  }
}
```

**Pros**:
- Could hold other uncertainty metrics (variance, bounds)
- Doesn't mix with provenance in mechanism

**Cons**:
- Confidence is intrinsically about *how* we know (mechanism)
- Adds top-level field (increases schema complexity)
- Would need to be optional everywhere

**Why Rejected**: Confidence is a property of derivation (mechanism),
not of the triple itself. Keeping it in mechanism is more semantically
correct and localized.

### Alternative 2: Enum Buckets

```json
"confidence": "high"  // or "medium", "low"
```

**Pros**:
- Simpler (no float precision issues)
- Forces categorization

**Cons**:
- Loss of precision (0.87 vs 0.88 vs 0.89 all = "high"?)
- Arbitrary thresholds (where does "high" start?)
- Can't do probabilistic reasoning (Bayesian updates)

**Why Rejected**: Numeric confidence is standard in ML/probabilistic
systems. Buckets can be derived from floats but not vice versa.
```

---

### 5. Impact Assessment

**Goal**: Help reviewers understand consequences

**Questions to answer**:
- Breaking change? (Do implementations need to change?)
- Performance impact?
- Security implications?
- Complexity added?

**Example**:
```markdown
## Impact Assessment

### Backward Compatibility

**Not a breaking change**:
- Field is optional
- Existing SPOC-M instances remain valid
- Systems not using confidence can ignore it

### Implementation Impact

**K-OS Systems**: Must
- Update SPOC-M validator to accept confidence field
- Optionally use confidence in reasoning

**Tooling**:
- compliance-suite: Add validation test cases
- kos-ce: Demonstrate confidence usage in examples

### Performance

Negligible:
- One additional float field (~8 bytes)
- No computation required (storage only)

### Complexity

Low:
- Well-understood concept (probabilities)
- Clear semantics (0-1 range)
- No interaction with other fields
```

---

### 6. Migration Path (If Breaking)

**Goal**: Minimize pain for adopters

**Include**:
- Deprecation timeline
- Compatibility shims
- Tools to aid migration

**Example**:
```markdown
## Migration Path

### Deprecation Schedule

1. **v2.5** (Current): Old and new syntax both valid
2. **v2.6-3.0** (1 year): Old syntax deprecated (warnings)
3. **v3.0** (Breaking): Old syntax removed

### Compatibility Mode

For 1 year, implementations can:
```python
if "old_field" in spoc_m:
    # Auto-migrate to new field
    spoc_m["new_field"] = convert(spoc_m["old_field"])
```

### Migration Tool

Provide `wekaou-migrate` script:
```bash
wekaou-migrate --from 2.5 --to 3.0 data.json
```
```

---

## Writing Tips

### Do

- **Start with a draft**: Get ideas down, refine later
- **Get early feedback**: Share in Discussions before formal RFC
- **Use concrete examples**: Abstract = confusing
- **Link to prior art**: "Similar to X in system Y"
- **Update based on feedback**: RFCs evolve through discussion
- **Be concise**: Respect reviewers' time

### Don't

- **Propose multiple changes**: One RFC = one logical change
- **Use jargon without explanation**: Not everyone knows your domain
- **Ignore alternatives**: "This is the only way" is rarely true
- **Take criticism personally**: Focus on ideas, not ego
- **Rush to voting**: Let discussion mature organically

---

## The Checklist

Before submitting, ask yourself:

- [ ] Can someone implement this without asking me questions?
- [ ] Have I considered at least 2 alternatives?
- [ ] Are there concrete examples?
- [ ] Is the impact on existing systems clear?
- [ ] Did I explain the *why*, not just the *what*?
- [ ] Is this one focused change (not a bundle)?

---

## Examples of Great RFCs

_Once we have accepted RFCs, we'll link exemplary ones here._

---

## Questions?

Ask in [wekaou-community](https://github.com/zaste/wekaou-community/discussions) with tag `rfc-help`.
