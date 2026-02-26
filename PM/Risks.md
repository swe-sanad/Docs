# Risk Management Framework

## Risk Categories
- Governance
- Technical
- Data Migration
- Operational
- Financial
- Personal / Delivery Risk

## Risk Register

| Risk ID | Category      | Probability | Impact | Risk Level | Description | Mitigation | Owner | Status |
|--------|--------------|-------------|--------|------------|-------------|------------|-------|--------|
| R1     | Governance   | High        | High   | Critical   | Informal requirement gathering may miss edge cases from billing, mediation, provisioning. | Formal workshop per domain, sign-off per module | You   | Open   |
| R2     | Technical    | Medium      | Very High | Critical | Legacy vendor data export limitations may cause data loss. | Early schema mapping, dry-run migration | You | Open |
| R3     | Financial    | Medium      | Very High | Critical | Rating or billing miscalculation in MVP stage. | Parallel billing run, invoice comparison before go-live | Finance + You | Open |
| R4     | Governance   | High        | High   | High       | Feature expansion before MVP stabilization. | Define MVP boundary formally, change control log | You | Open |
| R5     | Delivery     | High        | Very High | Critical | Entire project depends on one engineer. | Documentation discipline, architecture decisions recorded, consider secondary developer | You | Open |
| R6     | Organizational | Medium    | Medium | Medium     | Operational resistance. | Early demos, process alignment workshops | You | Open |
| R7     | Technical    | High        | High   | High       | Integration complexity (provisioning/mediation). | Define integration contracts early, mock provisioning APIs | You | Open |

## Probability × Impact Matrix

| Impact ↓ / Probability → | Low (1) | Med (2) | High (3) |
|-------------------------|---------|---------|----------|
| Low (1)                 | 1       | 2       | 3        |
| Medium (2)              | 2       | 4       | 6        |
| High (3)                | 3       | 6       | 9        |

Severity: 1–3 Low, 4–6 Medium, 7–9 Critical

## Project Special Considerations
- No formal governance structure
- Single developer execution
- Live revenue system replacement
- Biggest risk: uncontrolled evolution + fatigue
