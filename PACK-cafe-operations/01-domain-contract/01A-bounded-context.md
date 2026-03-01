# Bounded Context: Cafe Operations (Операции кофейни)

---

## Domain Name

**Русский:** Операции кофейни
**English:** Cafe Operations
**Scope:** Operations domain of VK-offee coffee shop network

---

## Object of Description

**Object:** The repeatable system of preparation, service, and delivery of beverages and food items in a coffee shop context.

| Object IS | Object IS NOT |
|-----------|---------------|
| A reproducible operational process with measurable parameters (time, temperature, weight) | Biography of individual barista or their skill development |
| A system of roles, methods, and work products | A training manual or teaching scenario |
| A standardized set of distinctions, entities, and methods | A customer experience guide or marketing material |
| A formal specification of cafe operations | Instructions on "how to learn" or procedural walkthrough |

**FPF Anchor:** This domain applies **A.1 (Holonic Foundation)** — the cafe is modeled as a holon: a whole system within itself AND a component of the VK-offee network.

---

## Scope (What's In)

| Element | Description | Example |
|---------|-------------|---------|
| **Roles** | Formal role definitions with clear responsibilities and state spaces | Barista, Cashier, Shift Manager |
| **Methods** | Repeatable procedures for creating beverages and food | Espresso extraction, Cappuccino preparation, Milk steaming |
| **Work Products** | Tangible outputs with existence criteria | Finished cappuccino (with crema, milk foam, volume spec) |
| **Failure Modes** | Known ways operations can fail, with detection tests | Under-extracted espresso (tasting bitter, extraction time < 25s) |
| **Domain Entities** | Core concepts of cafe operations | Product (drink/food), Ingredient, Equipment, Shift |
| **Distinctions** | Strict separations to avoid conceptual errors | Role ≠ Method ≠ Work; Menu ≠ Recipe; Order ≠ Served item |
| **SoTA (State-of-the-Art)** | Best current knowledge about cafe operations | Specialty coffee extraction standards, temperature profiles |

**FPF Anchor:** **A.1.1 (U.BoundedContext)** — all terms have local meaning within this cafe operations domain.

---

## Non-Goals (What's Out)

| Excluded | Reason | Where It Belongs |
|----------|--------|------------------|
| Customer experience design | Domain is operations, not customer psychology | F1-Suprasystem-Entrepreneur (market/customer analysis) |
| Staff training methodology | How to teach roles, not roles themselves | F9-Constructor-Manager (team methodology) |
| Business strategy and pricing | Financial decisions, not operational execution | F4-SoI-Entrepreneur (business requirements) |
| Equipment design/engineering | How machines are built, not how we use them | F5-SoI-Engineer (system architecture) |
| Supply chain management | Procurement and logistics, not cafe operations | F2-Suprasystem-Engineer (external interfaces) |

**FPF Anchor:** **A.1.1** — clear boundaries prevent scope creep and maintain semantic precision.

---

## Truth Criteria

Assertions in this pack are considered justified if they meet these criteria:

| Criterion | Test | Example |
|-----------|------|---------|
| **Observable Indicators** | Can we directly measure or detect the claim? | "Cappuccino is ready" = visual (foam height), auditory (machine stops), temporal (time elapsed) |
| **Verifiable Work Products** | Does the method produce a tangible output meeting specific criteria? | Flat White: 150ml milk + 30ml espresso, milk foam <5mm, served in 160ml cup |
| **Distinction Test** | Can we tell this concept apart from similar ones using observable differences? | Flat White ≠ Cappuccino: foam height ≤5mm vs ≥10mm |
| **SoTA + Revision Criterion** | Is there a known standard, AND do we know when to update it? | Espresso extraction: 25-30s per WBC standard; revise if cupping shows improvement |

**Forbidden in this pack:**
- Assertions without observable indicators (e.g., "barista is experienced" without measurable definition)
- Methods that don't produce defined work products (e.g., "make it taste good" — not specific enough)
- Distinctions that are purely semantic without operational difference
- SoTA claims without a revision criterion (e.g., outdated information not marked for update)

**FPF Anchor:** **B.3 (Trust & Assurance Calculus F-G-R)** — all claims require:
- **F (Formality):** Method description level (how formally specified)
- **G (Scope):** What conditions this applies to (espresso only? all drinks?)
- **R (Reliability):** Evidence supporting the claim (WBC standard? internal testing?)

---

## Downstream Note

**What this pack describes:** Cafe operations as they exist — the repeatable system of roles, methods, and work products.

**What downstream systems use:** Implementations may apply this knowledge differently:

| Pack Describes | Downstream Uses (outside scope) |
|---|---|
| "Barista role includes: espresso extraction" | Training curriculum (how to teach the role) — in F9-Constructor-Manager |
| "Cappuccino method: inputs=espresso+milk, output=180ml beverage" | Customer order system (how customers request drinks) — in F4-SoI-Entrepreneur |
| "Failure mode: over-extraction (>35s)" | Quality assurance process (how to detect and prevent) — in F6-SoI-Manager |
| "SoTA: WBC espresso extraction standard" | Equipment calibration procedure (how to implement the standard) — in F8-Constructor-Engineer |

**FPF Anchor:** **A.7 (Strict Distinction)** — we describe WHAT exists, not HOW to teach it, use it, or build it.

---

## Key Distinctions

These 12 core distinctions prevent conceptual errors in cafe operations:

| Distinction ID | In This Pack | Definition |
|---|---|---|
| **D01** | Role ≠ Method | A Barista (role) performs Espresso Extraction (method); they are not the same concept |
| **D02** | Method ≠ Work | Cappuccino (method/recipe) is abstract; a specific cappuccino served at 14:32 (work) is concrete |
| **D03** | Work Product ≠ Failure Mode | A successful cappuccino (WP) vs. a burnt milk cappuccino (FM) — both are observable, distinct outcomes |
| **D04** | Menu ≠ Recipe | Menu (customer-facing list) ≠ Recipe (internal operational specification) |
| **D05** | Ingredient ≠ Input | An ingredient is raw material; an input to a method is a measured ingredient at a specific state |
| **D06** | Order ≠ Served Item | Customer order (intent) ≠ completed drink (actual work product) |
| **D07** | Equipment State ≠ Readiness | Machine is at 92°C (state) ≠ Machine is ready to pull shots (readiness = state + calibration + time) |
| **D08** | Shift ≠ Work | A shift (time block, role assignment) ≠ work (specific tasks completed during shift) |
| **D09** | Standard ≠ Variation | WBC extraction standard (25-30s) ≠ operator-specific variation (26-28s for particular skill level) |
| **D10** | Capability ≠ Performance | A barista has espresso-extraction capability; a specific extraction shows actual performance |
| **D11** | Consistency ≠ Reproducibility | "Tastes the same" (subjective) ≠ "Same measurable parameters" (objective reproducibility) |
| **D12** | Maintenance ≠ Operation | Machine maintenance (repair, calibration) ≠ machine operation (pulling shots); different role scope |

---

## Domain Entities (Preliminary List)

Detailed specifications in `02-domain-entities/`:

| Entity Kind | Examples | Defined In |
|---|---|---|
| **Roles** | Barista, Shift Manager, Cashier, Head Chef | 02A-roles.md |
| **Products** | Espresso, Cappuccino, Flat White, Americano, Pastry | 02B-products.md |
| **Methods** | Espresso Extraction, Milk Steaming, Drink Assembly | 03-methods/ |
| **Work Products** | Finished Cappuccino, Receipt, Daily Report | 04-work-products/ |
| **Failure Modes** | Over-extraction, Under-extraction, Cold milk, Burnt milk | 05-failure-modes/ |
| **Resources** | Coffee beans, Milk, Cup, Filter basket, Water | (linked to resources subsystem) |
| **Devices** | Espresso machine, Grinder, Milk frother, POS terminal | (linked to equipment subsystem) |

---

## Version

| Attribute | Value |
|---|---|
| **Document ID** | CAFE.01A-bounded-context |
| **Version** | 1.0.0 (Initial) |
| **Created** | 2026-03-01 |
| **Last Updated** | 2026-03-01 |
| **Pack ID** | PACK-cafe-operations |
| **FPF Patterns Applied** | A.1, A.1.1, A.2, A.3, A.7, B.3, C.3 |
| **Status** | Ready for Review |

---

**Next Step:** See `01B-distinctions.md` for full specification of the 12 core distinctions.
