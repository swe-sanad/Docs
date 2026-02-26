
## Full List

| UC ID         | Title                        | Domain                        | Primary Actor | Status   |
|---------------|------------------------------|-------------------------------|---------------|----------|



## Use Case Template

### 1. Use Case Identification

| Field | Value |
|-------|--------|
| UC ID | UC-CA-01 |
| Title | Create User |
| Related FRs | FR-CA-01 |
| Domain | Customer & Account Management |
| Primary Actor | Admin/User |
| Supporting Actors | System |
| Level | User Goal |
| Status | Draft |
| Priority | Must |

---

### 2. Brief Description
A user or admin creates a new user account in the system.

---

### 3. Preconditions
- User is authenticated (if admin)
- Required registration fields are available

---

### 4. Trigger
User or admin initiates account creation.

---

### 5. Main Success Scenario (Basic Flow)
| Step | Actor Action | System Response |
|------|--------------|----------------|
| 1 | Fill registration form | Validate input |
| 2 | Submit form | Create user account |
| 3 |  | Confirm account creation |

---

### 6. Alternate Flows / Exceptions
#### A1 – Missing Required Fields
| Step | Actor Action | System Response |
|------|--------------|----------------|
| 1 | Submit incomplete form | Show error message |

---

<!-- Repeat the above block for each UC, changing the details as per the UC. -->



---

## Use Case Template

### 1. Use Case Identification

| Field | Value |
|-------|--------|
| UC ID | UC-XXX |
| Title | Short Descriptive Name |
| Related FRs | FR-XXX, FR-YYY |
| Domain | (e.g., Audit Logging / IAM) |
| Primary Actor | |
| Supporting Actors | |
| Level | User Goal / System |
| Status | Draft / Approved |
| Priority | Must / Should / Could |

---

### 2. Brief Description
A short summary of the goal the actor achieves.

---

### 3. Preconditions
- User/system state required before execution.
- Required permissions.
- Required configuration.

---

### 4. Trigger
Event that initiates the use case.

---

### 5. Main Success Scenario (Basic Flow)
| Step | Actor Action | System Response |
|------|--------------|----------------|
| 1 | | |
| 2 | | |
| 3 | | |

---

### 6. Alternate Flows / Exceptions
#### A1 – Alternate Condition Name
- Condition:
- Flow:
  1.
  2.

#### E1 – Error Condition
- Condition:
- System Response:

---

### 7. Postconditions
#### Success Postconditions
- System state after successful completion.
#### Failure Postconditions
- System state if aborted.

---

### 8. Business Rules
- BR-001:
- BR-002:

---

### 9. Non-Functional Requirements Impacted
- Performance:
- Logging:
- Security:
- Availability:

---

### 10. UI / API Notes (Optional)
- UI screen references
- API endpoint
- Payload structure
