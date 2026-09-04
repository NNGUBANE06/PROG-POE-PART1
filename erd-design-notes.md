# RaceDay - Entity Relationship Diagram: Design Notes

This document describes the entities, attributes, and relationships that make up the RaceDay database design. It accompanies the visual ERD (`erd.png`) in this folder.

## Entities & Attributes

### 1. Roles
- RoleID (PK)
- RoleName *(e.g. "Admin", "Participant")*

### 2. Users
- UserID (PK)
- FullName
- Email (unique)
- PasswordHash
- RoleID (FK → Roles)
- CreatedAt

### 3. Events
- EventID (PK)
- EventName
- EventDate
- Location
- Description
- CreatedBy (FK → Users) — the Admin/organizer who created the event

### 4. Categories
- CategoryID (PK)
- EventID (FK → Events)
- CategoryName *(e.g. "10km", "21km")*
- Distance
- MaxParticipants

### 5. Enrolments
- EnrolmentID (PK)
- UserID (FK → Users)
- CategoryID (FK → Categories)
- EnrolmentDate
- Status *(pending/confirmed/cancelled)*

### 6. Results
- ResultID (PK)
- EnrolmentID (FK → Enrolments, unique)
- FinishTime
- Position
- Status *(finished/DNF/DQ)*

## Relationships & Cardinality

| Relationship | Cardinality | Notes |
|---|---|---|
| Roles → Users | One-to-many | One role is assigned to many users |
| Users → Events | One-to-many | One Admin user can create many events |
| Events → Categories | One-to-many | One event contains many categories |
| Users ↔ Categories | Many-to-many | Resolved through the **Enrolments** junction table — a user enrols in many categories, and a category has many enrolled users |
| Enrolments → Results | One-to-one | Each enrolment produces at most one result |

## Design Notes

- **Roles** is modelled as its own entity rather than a plain text field on Users, to clearly demonstrate role-based system design.
- The **many-to-many** relationship between Users and Categories is resolved through the **Enrolments** junction table rather than drawn as a direct link — this reflects standard relational database normalization.
- **CreatedBy** on Events is a foreign key back to Users, identifying the Admin/organizer who created the event.
