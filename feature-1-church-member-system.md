# Feature: Title

**Feature ID:** 1
**Branch pattern:** `feature/1-church-member-system`  
**Status:** Draft
**Created:** 2026-09-14
**Input:** Manage and track church member attendance  
**Depends on:** None
**Related:** None

---

## User Stories

### US-1.1: Register as a Church Member
**As a** New Church Member  
**I want to** Register my information with the church easily via my phone, kiosk, or employee.
**So that** I can easily attend church and help the church attendance statistics.

**Priority:** P1  
**Independent test:** New member can sign up as a church member without assistance. 
**Acceptance scenarios:** see ### US-1.1 under Acceptance Criteria

### US-1.2: Track Church Attendance
**As a** stakeholder 
**I want to** know how many people attended church
**So that** I know if we are gowing or shrinking

**Priority:** P3
**Independent test:** Stakeholder can view church attendance over a specificed amount of time
**Acceptance scenarios:** see ### US-1.2 under Acceptance Criteria

### US-1.3: Member Church Attendance
**As a** Church Member
**I want to** mark myself as present at church
**So that** I can be marked as present

**Priority:** P1
**Independent test:** A church member can mark themselves as present if they are there during church
**Acceptance scenarios:** see ### US-1.2 under Acceptance Criteria

### US-1.4: Church Member Profile
**As an** employee  
**I want to** know basic information about a member
**So that** I have a complete profile on the member that can be used for specific chruch functions. (Member pickup, Auto giving, child identification, etc)

**Priority:** P1  
**Independent test:** Employee can access all given (uncompromising) information on member
**Acceptance scenarios:** see ### US-1.4 under Acceptance Criteria

### US-1.5: Driver Route
**As an** driver  
**I want to** what route to take to pickup my assigned members
**So that** I can bring them to chruch safely and efficiently

**Priority:** P2
**Independent test:** Driver can get or generate a van route to pick up their assigned members
**Acceptance scenarios:** see ### US-1.5 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST track member attendance
- **FR-002**: Users MUST be able to register with their information
- **FR-003**: Employees MUST be able to edit member information
- **FR-004**: Children MUST be able to be identified and be attached to a parent
- **FR-005**: Users MUST be able to use the system anywhere
- **FR-006**: System must be secure and keep PII safe

---

## Data Model Requirements

### `Member` table
| Field              | Type       | Rules                                                                 |
| ------------------ | ---------- | --------------------------------------------------------------------- |
| `id`               | INTEGER PK | Auto-increment                                                        |
| `Name`             | String     |                                                                       |
| `Address`          | String     |                                                                       |
| `Phone`            | Integar    | 10 Digit Number                                                       |
| `Email`            | String     | have @ and a domain                                                   |
| `isChild`          | Boolean    | dependant of `age`                                                    |
| `firstContactDate` | DateTime   |                                                                       |
| `isBaptized`       | Boolean    |                                                                       |
| `age`              | Integar    | dependant of `birthday`                                               |
| `birthday`         | Date       |                                                                       |
| `gender`           | String     | must be `male` or `female`                                            |
| `classes`          | String[]   | Each string must match class id                                       |
| `parent`           | Integar    | Parent's `Member` id                                                  |
| `attendingSchool`  | String     | Attending school, can be null                                         |
| `password`         | String     | SHA-256 Hash                                                          |
| `AccountType`      | String     | Must be: MEMBER, TEACHER,<br>DRIVER, EMPLOYEE, MANAGER,<br>or, ADMIN. |
|                    |            |                                                                       |
### `DriverRoute` table
| Field              | Type       | Rules                       |
| ------------------ | ---------- | --------------------------- |
| `id`               | INTEGER PK | Auto-increment              |
| `Driver`           | Integar    | Assigned Driver             |
| `Addresses`        | Integar[]  | Member Id in order to route |


---

## Acceptance Criteria

### US-1.1 — Register as a Church Member

#### Scenario: Person is registered as a Member
*   **Given** Person is not in system
*   **When** employee or person adds the person to the system
*   **Then** Person is a member in system
*   **And** extra result if needed

#### Scenario: Failure to create Member
*   **Given** Person is not in system
*   **When** employee or person adds the person to the system
*   **Then** Person is not a member in the system

### US-1.2 — Track Member Attendance

#### Scenario: Member Attendance Logging
*   **Given** Member is in Church Member Database
*   **When** Member attends Church
*   **Then** Attendance is logged

#### Scenario: Failure to Log Attendance
*   **Given** Member is in Church Member Database 
*   **When** Member attends Church
*   **Then** Attendance is not logged

#### Scenario: Faked Attendance Logged
*   **Given** Member is in Church Member Database 
*   **When** Member does not attend Church
*   **Then** Attendance is logged
### US-1.4: Church Member Profile

#### Scenario: Access Member Data
*   **Given** Member is in Church Member Database
*   **When** employee needs to access personal member data
*   **Then** Person data is available
*   **And** extra result if needed

#### Scenario: Failure to Access Member Data
*   **Given** Member is in Church Member Database
*   **When** employee needs to access personal member data
*   **Then** employee cannot access personal member data

### US-1.5: Driver Route

#### Scenario: Successful Route Request
*   **Given** Driver route is created
*   **When** driver requests the route
*   **Then** system responds with a route of addresses
*   **And** extra result if needed

#### Scenario: Faulty Route Request
*   **Given** Driver route is created
*   **When** driver requests the route
*   **Then** system responds with incorrect route or no route

