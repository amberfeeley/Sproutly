# Stated Requirements (SA&D) — Sproutly

This document defines **what the system must do** (Functional Requirements) and the
quality attributes/constraints it must satisfy (Non-Functional Requirements), without
implementation details.

---

## 1. Purpose

Sproutly helps users plan and manage gardens by capturing garden parameters,
evaluating suitability against environmental factors and reference data, and producing
actionable recommendations and planning outputs.

---

## 2. Scope

### 2.1 In Scope
- User account creation and login
- Garden management (create/view/update/delete a garden profile)
- Plant management (add/update/remove plants associated with a garden)
- Planting recommendations based on user inputs and reference data
- Generation of a personalized garden calendar
- Persistence of user and garden information
- Basic reporting outputs: recommendations, calendar, suitability notes, estimates

### 2.2 Out of Scope (v1)
- Payments/subscriptions
- Social features (sharing, community, comments)
- E-commerce / seed purchasing integrations
- IoT sensor integration / real-time telemetry
- Mobile native applications (unless later approved)
- Advanced analytics/ML model training (beyond rules/logic-based evaluation)

---

## 3. Assumptions
- Users provide accurate location and garden parameters.
- Reference data sources (e.g., weather/zone/soil) are available and sufficiently reliable.
- “Recommendations” are guidance and do not guarantee outcomes.
- The system will support at least one reference source per category (zone/weather/soil) in v1.

---

## 4. Actors
- **User**: creates an account, logs in, manages gardens, manages plants, views outputs.
- **External Validation/Reference Services**: authoritative sources used to validate or enrich inputs
  (e.g., email validation, zone/weather/soil reference data).

---

## 5. Functional Requirements (FR)

> Format: **FR-###** — The system shall …

### 5.1 Account & Access
- **FR-001** — The system shall allow a user to create an account.
- **FR-002** — The system shall allow a user to log in using their account credentials.
- **FR-003** — The system shall restrict access to protected features unless the user is authenticated.

### 5.2 Garden Management
- **FR-010** — The system shall allow an authenticated user to create a garden profile.
- **FR-011** — The system shall allow an authenticated user to view their garden profiles.
- **FR-012** — The system shall allow an authenticated user to update a garden profile.
- **FR-013** — The system shall allow an authenticated user to delete a garden profile.

### 5.3 Plant Management
- **FR-020** — The system shall allow an authenticated user to manage plants associated with a garden.
- **FR-021** — The system shall allow an authenticated user to add a plant to a garden.
- **FR-022** — The system shall allow an authenticated user to update a plant associated with a garden.
- **FR-023** — The system shall allow an authenticated user to remove a plant from a garden.

### 5.4 Location & Reference Data Use
- **FR-030** — The system shall accept location data (e.g., ZIP code or GPS coordinates) as input to planning.
- **FR-031** — The system shall determine a suitable plant hardiness zone (or equivalent zone classification) from the user’s location.
- **FR-032** — The system shall use weather-related information to assess planting timing risk (e.g., frost timing/risk).
- **FR-033** — The system shall use soil-related information, when available, to support suitability assessment.

### 5.5 Recommendations & Planning Outputs
- **FR-040** — The system shall generate actionable planting recommendations for a garden (e.g., plant now, start indoors, wait).
- **FR-041** — The system shall generate a personalized garden calendar for a garden.
- **FR-042** — The system shall present a suitability summary explaining key factors influencing recommendations (location/zone, weather, soil, and user parameters).
- **FR-043** — The system shall provide estimates useful for planning (e.g., acreage/space planning estimates) when relevant inputs are provided.

### 5.6 Data Persistence
- **FR-050** — The system shall store user profile information.
- **FR-051** — The system shall store garden profiles and associated plants.
- **FR-052** — The system shall allow users to retrieve previously saved gardens and planning outputs.

---

## 6. Non-Functional Requirements (NFR)

> Format: **NFR-###** — The system shall …

### 6.1 Security & Privacy
- **NFR-001** — The system shall authenticate users before allowing access to protected features.
- **NFR-002** — The system shall enforce access control so users can only access their own gardens and plants.
- **NFR-003** — The system shall protect user credentials and sensitive data in storage and transit (implementation details defined in Software Design).

### 6.2 Reliability & Availability
- **NFR-010** — The system shall handle temporary unavailability of external reference services gracefully (e.g., provide partial output or a clear message).
- **NFR-011** — The system shall avoid data loss for saved user, garden, and plant records under normal operation.

### 6.3 Usability
- **NFR-020** — The system shall present recommendations and calendar outputs in a clear, understandable format.
- **NFR-021** — The system shall provide user-friendly feedback for invalid inputs (details documented as alternate flows in activity diagrams).

### 6.4 Performance
- **NFR-030** — The system shall produce recommendations and calendar outputs within a reasonable time for typical use (specific targets defined in Software Design).

### 6.5 Maintainability
- **NFR-040** — The system shall keep analysis artifacts and design artifacts separated according to the repository documentation structure.

---

## 7. Constraints
- **C-001** — SA&D artifacts must not include implementation-specific details (APIs, schemas, frameworks).
- **C-002** — PlantUML source diagrams must be stored as `.puml`; rendered exports for GitHub display must be stored under `docs/diagrams/`.

---

## 8. Traceability (IPO → Requirements)

### Inputs
- Location data → FR-030, FR-031
- User preferences & garden parameters → FR-010–FR-013, FR-040–FR-043
- External reference data (zone/weather/soil) → FR-031–FR-033

### Processing
- Zone lookup → FR-031
- Weather/frost risk analysis → FR-032
- Soil suitability support → FR-033
- Suitability evaluation & planning → FR-040–FR-043
- Persistence → FR-050–FR-052

### Outputs
- Recommendations → FR-040, FR-042
- Calendar → FR-041
- Suitability summary → FR-042
- Estimates → FR-043
- Saved dashboards/history → FR-052
