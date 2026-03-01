# Ontology: Cafe Operations Domain

**Formal definition of core concepts (Kinds) and their relationships.**

FPF Patterns: **C.3 (Kind-CAL)**, **A.2.1 (U.RoleAssignment)**

---

## Root Holon: CAFE-OPERATIONS

```
CAFE-OPERATIONS (Holon)
├─ ACTOR → who does work
├─ ROLE → assignment of responsibilities
├─ METHOD → how to produce output
├─ WORK → concrete execution
├─ WORK-PRODUCT → tangible output
├─ FAILURE-MODE → ways to fail
├─ INGREDIENT → raw materials
├─ INPUT → prepared for method
├─ EQUIPMENT → physical devices
├─ SHIFT → time block with roles
└─ ORDER → customer request
```

---

## Core Kinds (Type Definitions)

### ACTOR (Agent)
**Definition:** Entity capable of holding roles and performing work.

**Specializations:**
- HUMAN-ACTOR (barista, manager, customer)
- SYSTEM-ACTOR (POS, timer)

**Properties:**
- identifier: String
- capabilities: Set[CAPABILITY]
- role_assignment_context: CONTEXT

---

### ROLE (Kind)
**Definition:** Persistent set of responsibilities and authorities assigned to an actor.

**Specializations:**
- BARISTA (espresso extraction, milk steaming)
- SHIFT-MANAGER (coordination, quality oversight)
- CASHIER (payments, orders)
- HEAD-CHEF (food preparation, menu design)

**Properties:**
- role_name: String
- responsibilities: Set[RESPONSIBILITY]
- authorities: Set[AUTHORITY]
- state_graph: ROLE-STATE-GRAPH
- required_capabilities: Set[CAPABILITY]

**FPF Anchor:** F.4 (Role Description)

---

### METHOD (Kind)
**Definition:** Abstract, repeatable procedure for transforming inputs into specified output.

**Specializations:**
- BEVERAGE-METHOD (Espresso, Cappuccino, Flat-White)
- FOOD-METHOD (Pastry-Warming, Sandwich-Assembly)
- MAINTENANCE-METHOD (Machine-Descaling, Grinder-Calibration)

**Properties:**
- method_id: String (e.g., "CAFE.METHOD.001")
- name: String
- inputs: Ordered[INPUT]
- outputs: Ordered[OUTPUT]
- duration: Duration (e.g., 25-30 seconds)
- preconditions: Set[CONDITION]
- postconditions: Set[CONDITION]
- failure_modes: Set[FAILURE-MODE]

**FPF Anchor:** A.3.1 (U.Method)

---

### WORK (Kind)
**Definition:** Concrete occurrence of METHOD execution at specific time by specific ACTOR.

**Properties:**
- work_id: Unique ID (timestamp + sequence)
- method_ref: METHOD
- actor_ref: ACTOR
- start_time: Timestamp
- end_time: Timestamp
- actual_duration: Duration
- input_refs: Set[INPUT]
- output_ref: WORK-PRODUCT | FAILURE-MODE
- quality_assessment: PASS | FAIL

**FPF Anchor:** A.15.1 (U.Work)

---

### WORK-PRODUCT (Kind)
**Definition:** Tangible output of successful METHOD execution, meeting all existence criteria.

**Specializations:**
- BEVERAGE (Espresso, Cappuccino, Flat-White)
- FOOD-ITEM (Pastry, Sandwich)
- DOCUMENT (Receipt, Daily-Report)

**Properties:**
- product_id: Unique ID
- product_kind: KIND
- existence_criteria: Set[CRITERION]
- measurements: Map[MEASURE → VALUE]
- created_by_work: WORK
- served_to: ACTOR | null
- service_time: Timestamp

**Example Criteria for Cappuccino:**
- foam_height: 8-12mm
- crema: present
- temperature: 60-70°C
- volume: 155-165ml

---

### FAILURE-MODE (Kind)
**Definition:** Observable way METHOD execution fails to produce conforming WORK-PRODUCT.

**Specializations:**
- EXTRACTION-FAILURE (Over-extraction, Under-extraction, Channeling)
- MILK-FAILURE (Burnt-milk, Cold-milk, Flat-foam)
- ASSEMBLY-FAILURE (Wrong-portion, Contamination, Temperature-loss)

**Properties:**
- failure_id: String (e.g., "CAFE.FAIL.001")
- name: String
- method_ref: METHOD
- detection_test: TESTABLE (observable condition)
- observable_indicators: Set[INDICATOR]
- root_causes: Set[CAUSE]
- remediation: TEXT

**Example (Over-extraction):**
- detection_test: "extraction_time > 35s OR taste_bitter"
- indicators: {dark-color, bitter-taste, thin-crema}
- causes: {wrong-dose, high-temp, stale-beans}

---

### INPUT (Kind)
**Definition:** Prepared element — measured, at correct condition — ready for METHOD execution.

**Specializations:**
- INGREDIENT-INPUT (Coffee, Milk, Water)
- CONDITION-INPUT (Equipment-ready, Environment-acceptable)

**Properties:**
- input_id: Unique ID
- quantity: MEASURE
- state: STATE
- quality_gate: GATE
- ingredient_source: INGREDIENT
- consumed_by_work: WORK

**Example:**
- Coffee-input: 18g, freshly-ground, <5min-old
- Milk-input: 120ml, 4°C, opened <7days

**FPF Anchor:** D05 (Ingredient ≠ Input)

---

### INGREDIENT (Kind)
**Definition:** Raw material in inventory form, not yet prepared for specific method.

**Specializations:**
- COFFEE-BEANS
- MILK
- WATER
- PASTRY-ITEMS

**Properties:**
- ingredient_id: String
- name: String
- supplier: STRING
- quantity_onhand: MEASURE
- quality_spec: SPECIFICATION
- storage_condition: CONDITION
- expiry_info: DATE | null

---

### EQUIPMENT (Kind)
**Definition:** Physical device used in METHOD execution, with measurable state and readiness.

**Specializations:**
- ESPRESSO-MACHINE
- GRINDER
- MILK-FROTHER
- POS-TERMINAL

**Properties:**
- device_id: String
- device_type: KIND
- state_model: STATE-GRAPH
- current_state: STATE
- readiness: BOOLEAN
- readiness_checks: Set[CHECK]
- maintenance_schedule: SCHEDULE
- last_maintenance: Timestamp

**State vs. Readiness Example:**
- State: {temp: 92.1°C, pressure: 9.0bar}
- Readiness checks: {temp-ok, pressure-ok, warm-up-complete, fault-free}
- Readiness result: true (all checks pass) OR false

**FPF Anchor:** D07 (Equipment State ≠ Readiness)

---

### SHIFT (Kind)
**Definition:** Time block with assigned roles and personnel, context for WORK to occur.

**Properties:**
- shift_id: String
- start_time: Timestamp
- end_time: Timestamp
- assigned_roles: Map[ROLE → ACTOR]
- work_performed: Set[WORK]
- quality_summary: SUMMARY (pass-rate, issues)

**Example:**
- Morning-shift: 06:00-14:00
  - barista: Maria
  - manager: Piotr
  - cashier: Elena

**FPF Anchor:** D08 (Shift ≠ Work)

---

### ORDER (Kind)
**Definition:** Customer's request/intent, recorded in system but not yet fulfilled.

**Properties:**
- order_id: String (e.g., "#4521")
- customer_ref: ACTOR
- ordered_items: List[ITEM-SPEC]
- order_time: Timestamp
- expected_ready_time: Timestamp
- status: ENUM {pending, in-progress, ready, served, cancelled}
- served_items: Set[WORK-PRODUCT]

**FPF Anchor:** D06 (Order ≠ Served Item)

---

### STANDARD (Kind)
**Definition:** Baseline specification accepted across organization, with revision criteria.

**Examples:**
- WBC-ESPRESSO-STANDARD: extraction 25-30s, yield 1:2, pressure 9bar
- CAPPUCCINO-SPEC: 30ml espresso, 120ml milk, 10mm foam

**Properties:**
- standard_id: String
- name: String
- applies_to: Set[METHOD]
- parameters: Map[PARAM → RANGE]
- authority: STRING
- revision_criterion: TEXT
- last_review: Timestamp

**FPF Anchor:** D09 (Standard ≠ Variation)

---

## Kind Relationships

### Composition
```
SHIFT composes WORK+
WORK consumes INPUT+
INPUT comes-from INGREDIENT
METHOD produces WORK-PRODUCT | FAILURE-MODE
ORDER triggers WORK+
```

### Role Enactment
```
ACTOR holds ROLE in SHIFT
ROLE requires CAPABILITY
CAPABILITY enables METHOD
```

### State/Readiness
```
EQUIPMENT has STATE
STATE + MAINTENANCE + TIME → READINESS
READINESS gates METHOD-execution
```

---

## Version

| Attribute | Value |
|---|---|
| **Document ID** | CAFE.01C-ontology |
| **Version** | 1.0.0 |
| **Created** | 2026-03-01 |
| **Pack ID** | PACK-cafe-operations |
| **FPF Patterns** | C.3, A.2.1, A.1, A.15.1 |
| **Status** | Ready |

---

**Next:** See `02-domain-entities/` for detailed specifications.
