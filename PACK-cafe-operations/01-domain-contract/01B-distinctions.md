# Distinctions: Cafe Operations Domain

**Core separation of concepts preventing category errors in cafe operations.**

FPF Pattern: **A.7 (Strict Distinction)**

---

## 12 Core Distinctions

### D01: Role ≠ Method
- **Role:** Persistent assignment to person (Barista)
- **Method:** Abstract procedure independent of who does it (Espresso Extraction)
- **Test:** Can different people do same method? Yes → It's a method

### D02: Method ≠ Work
- **Method:** Abstract recipe (Cappuccino formula)
- **Work:** Concrete execution at specific time (Cappuccino served 14:32)
- **Test:** Can this change while staying "same thing"? Methods yes (versioned), work no (immutable)

### D03: Work Product ≠ Failure Mode
- **Work Product:** Output meeting all existence criteria (successful cappuccino)
- **Failure Mode:** Output failing criteria (burnt milk)
- **Test:** Does this meet success criteria? Yes→WP, No→FM

### D04: Menu ≠ Recipe
- **Menu:** Customer-facing description ("Rich cappuccino")
- **Recipe:** Operational specification (30ml espresso + 120ml milk)
- **Test:** Would untrained person reproduce from this? Yes→Recipe, No→Menu

### D05: Ingredient ≠ Input
- **Ingredient:** Raw material in inventory (1L milk bottle)
- **Input:** Measured, prepared for method (120ml at 4°C, within shelf-life)
- **Test:** Is this raw or prepared for method?

### D06: Order ≠ Served Item
- **Order:** Customer request/intent (cappuccino, no sugar)
- **Served Item:** Completed work product delivered (cappuccino served 14:32)
- **Test:** Could order be canceled? Yes→Order. Served item be "un-served"? No→Served.

### D07: Equipment State ≠ Readiness
- **State:** Observable current condition (92°C, 9bar)
- **Readiness:** State + calibration + warm-up time (ready=all checks pass)
- **Test:** Can measure right now? State. Requires multiple checks? Readiness.

### D08: Shift ≠ Work
- **Shift:** Time block with assigned roles (Maria: Barista, 14:00-22:00)
- **Work:** Specific completed tasks (Order #4521: cappuccino, 14:32-14:35)
- **Test:** Fixed duration? Shift. Variable, task-based? Work.

### D09: Standard ≠ Variation
- **Standard:** Mandatory baseline (WBC: 25-30s extraction)
- **Variation:** Acceptable range within standard (Maria: 26-27s, New barista: 28-29s)
- **Test:** Mandatory or range?

### D10: Capability ≠ Performance
- **Capability:** Ability to perform under ideal conditions (certified espresso extraction)
- **Performance:** Actual execution results today (26.5s extraction this morning)
- **Test:** Can they do it? Capability. Did they? Performance.

### D11: Consistency ≠ Reproducibility
- **Consistency:** Subjective perception ("tastes the same")
- **Reproducibility:** Objective measurable parameters (26s±0.2s extraction)
- **Test:** Measurable? Reproducibility. Opinion-based? Consistency.

### D12: Maintenance ≠ Operation
- **Operation:** Regular use to produce work products (pulling shots)
- **Maintenance:** Upkeep/repair to sustain equipment (descaling, calibration)
- **Test:** Produces customer drinks? Operation. Sustains equipment? Maintenance.

---

## Distinction Relationships

```
D01 (Role ≠ Method)
├─→ D02 (Method ≠ Work)
│   ├─→ D03 (Work Product ≠ Failure Mode)
│   └─→ D06 (Order ≠ Served Item)
├─→ D04 (Menu ≠ Recipe)
└─→ D08 (Shift ≠ Work)

D05 (Ingredient ≠ Input) → D02 (Method ≠ Work)
D07 (Equipment State ≠ Readiness) → D01 (affects capability)
D09 (Standard ≠ Variation) → D10 (Capability ≠ Performance)
D11 (Consistency ≠ Reproducibility) → D10 (Capability ≠ Performance)
D12 (Maintenance ≠ Operation) → D01 (Role ≠ Method)
```

---

## Version

| Attribute | Value |
|---|---|
| **Document ID** | CAFE.01B-distinctions |
| **Version** | 1.0.0 |
| **Created** | 2026-03-01 |
| **Pack ID** | PACK-cafe-operations |
| **FPF Pattern** | A.7 (Strict Distinction) |
| **Status** | Ready |
