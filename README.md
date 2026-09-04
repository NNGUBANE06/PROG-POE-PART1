# RaceDay - Race Event Management System

## Description

RaceDay is a system for organizing and managing race events (marathons, trail runs, fun runs). It allows event organizers to create events and race categories, and allows participants to register, browse events, enrol in categories, and view their results. The system is built around a relational database (see `/docs/erd.png`), a planned RESTful API (see `/docs/endpoint-plan.md`), and a SQL Server schema (see `/docs/raceday_schema.sql`).

## Roles

**Admin (Organizer)**
Responsible for managing events. Admins can create, update, and delete events and categories, view and confirm participant enrolments, capture and correct race results, and manage user accounts.

**Participant**
A registered runner. Participants can browse available events and categories, manage their own profile, enrol in a category, view their own enrolments, and check their own results and category leaderboards.

## Repository Structure

```
/docs
  erd.png              - Entity Relationship Diagram for the RaceDay database
  endpoint-plan.md      - API endpoint specification table (Section B)
  raceday_schema.sql    - SQL script to create and populate the database (Section C)
/.github/workflows
  validate-structure.yml - GitHub Actions workflow validating repo structure
README.md
```

## CI/CD

A GitHub Actions workflow validates that the `/docs` folder exists and contains the required files (`erd.png`, `endpoint-plan.md`, `raceday_schema.sql`) on every push and pull request.

**Successful build screenshot:**

*[Insert screenshot of a green/passing GitHub Actions run here]*

## Video Walkthrough

An unlisted YouTube video walking through the planning documents, the ERD decisions, the endpoint plan, and the SQL script is available here:

**[Insert unlisted YouTube link here]**

## How to Run the SQL Script

1. Open SQL Server Management Studio (SSMS).
2. Connect to a clean SQL Server instance.
3. Open `docs/raceday_schema.sql`.
4. Execute the script (F5). It will create the `RaceDayDB` database, all tables, and sample data.
