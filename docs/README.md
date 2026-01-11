# Documentation Structure – Sproutly

This document defines the purpose, scope, and allowed contents of each documentation
folder in the Sproutly repository.

Sproutly enforces a **strict separation** between:

- **Systems Analysis & Design (SA&D)** – *what the system must do and why*
- **Software Design** – *how the system will be built*

This separation is intentional and exists to reduce ambiguity, prevent scope creep,
and maintain clarity as the project evolves.

---

## `docs/00-overview/` — Project Orientation

**Purpose:**  
Provide high-level, non-technical context and shared understanding.

**Audience:**  
Stakeholders, contributors, reviewers, and new collaborators.

### Allowed contents
- Project vision and goals
- Domain glossary
- Assumptions and constraints
- High-level decisions and rationale

### Not allowed
- Detailed requirements
- Diagrams
- Technical or implementation details

---

## `docs/10-analysis-sad/` — Systems Analysis & Design (SA&D)

**Purpose:**  
Define **what problem the system solves**, **what it must do**, and **under what
constraints**, without making implementation decisions.

**Audience:**  
System analysts, business stakeholders, auditors, and designers.

> If a non-technical stakeholder can reasonably review the artifact, it belongs here.

---

### `ipo.md`
Defines:
- Inputs
- Logical processes (conceptual, not technical)
- Outputs

**Must not include:**
- APIs
- Databases or schemas
- Code or frameworks

---

### `requirements.md`
Defines:
- Functional Requirements (FR)
- Non-Functional Requirements (NFR)
- Assumptions
- In-scope and out-of-scope items
- Constraints

Requirements are written in **“The system shall…”** format.

---

### `use-cases/`
Defines user goals and system capabilities.

**May include:**
- Use case diagram (`use-case-diagram.puml`)
- Textual use case descriptions (`uc-###-name.md`)
  - Main success flow
  - Alternate flows
  - Preconditions and postconditions

**Must not include:**
- Validation logic
- Error messages
- UI behavior
- Technical steps

---

### `activities/`
Defines logical workflows and behavior.

**May include:**
- Activity diagrams
- Decision points
- Alternate and error flows

**Must not include:**
- Method calls
- APIs
- Code-level logic

---

### `data/`
Defines data at a **conceptual level**.

**May include:**
- Logical Data Flow Diagrams (DFD)
- Conceptual ERDs (entities and relationships)

**Must not include:**
- Table schemas
- Column types
- Indexes
- SQL

---

### What must NOT appear anywhere in `10-analysis-sad/`
- Programming languages
- Frameworks
- APIs or endpoints
- Classes or methods
- Database schemas
- UI layouts

---

## `docs/20-software-design/` — Software Design

**Purpose:**  
Define **how the system will be built**, based on approved SA&D artifacts.

**Audience:**  
Developers, architects, and implementers.

> If a developer must review it to implement the system, it belongs here.

---

### `architecture.md`
- System layers and components
- Deployment model
- Technology stack decisions

---

### `sequence/`
- Detailed sequence diagrams
- Time-ordered interactions
- Service or API calls

---

### `api/`
- API specifications (e.g., OpenAPI)
- Endpoint definitions
- Request and response schemas

---

### `data/`
- Physical ERDs
- Database schemas
- SQL definitions

---

### `ui/`
- Wireframes
- Screen flows
- Navigation structure

---

### `adr/` — Architecture Decision Records
- Documented technical decisions
- Rationale and trade-offs
- Consequences of decisions

---

## `docs/diagrams/` — Rendered Diagram Artifacts

**Purpose:**  
Store exported diagram images for GitHub display.

GitHub does **not** render `.puml` files directly.

### Structure
docs/diagrams/
├─ analysis/ # SA&D diagrams (PNG/SVG)
└─ design/ # Software design diagrams (PNG/SVG)

Each rendered image should correspond to a `.puml` source file located elsewhere
in the documentation tree.

---

## Guiding Rule

> **If the question is “what must the system do?” — it is SA&D.**  
> **If the question is “how will we build it?” — it is Software Design.**

When in doubt, err toward **analysis first**.

---

## Status

This project is currently analysis-driven.  
Implementation artifacts will be introduced only after SA&D artifacts stabilize.
