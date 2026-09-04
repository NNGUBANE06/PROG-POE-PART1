# RaceDay API Endpoint Plan

Roles: **Admin** (event organizer) and **Participant** (registered runner).

## Authentication

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|---|---|---|---|---|---|
| POST | /api/auth/register | Registers a new user account | Public | `{ fullName, email, password }` | `201 Created` — `{ userId, email }` |
| POST | /api/auth/login | Authenticates a user and issues a token | Public | `{ email, password }` | `200 OK` — `{ token, userId, role }` |

## User Profile

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|---|---|---|---|---|---|
| GET | /api/users/me | Retrieves the logged-in user's profile | Admin, Participant | — | `200 OK` — `{ userId, fullName, email, role }` |
| PUT | /api/users/me | Updates the logged-in user's profile details | Admin, Participant | `{ fullName, email }` | `200 OK` — updated profile object |
| GET | /api/users/{id} | Retrieves a specific user's profile | Admin | — | `200 OK` — user object |

## Events

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|---|---|---|---|---|---|
| GET | /api/events | Lists all events | Admin, Participant | — | `200 OK` — array of event objects |
| GET | /api/events/{id} | Retrieves a single event's details | Admin, Participant | — | `200 OK` — event object |
| POST | /api/events | Creates a new event | Admin | `{ eventName, eventDate, location, description }` | `201 Created` — created event object |
| PUT | /api/events/{id} | Updates an existing event | Admin | `{ eventName, eventDate, location, description }` | `200 OK` — updated event object |
| DELETE | /api/events/{id} | Deletes an event | Admin | — | `204 No Content` |

## Categories

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|---|---|---|---|---|---|
| GET | /api/events/{eventId}/categories | Lists all categories for an event | Admin, Participant | — | `200 OK` — array of category objects |
| GET | /api/categories/{id} | Retrieves a single category's details | Admin, Participant | — | `200 OK` — category object |
| POST | /api/events/{eventId}/categories | Creates a new category under an event | Admin | `{ categoryName, distance, maxParticipants }` | `201 Created` — created category object |
| PUT | /api/categories/{id} | Updates an existing category | Admin | `{ categoryName, distance, maxParticipants }` | `200 OK` — updated category object |
| DELETE | /api/categories/{id} | Deletes a category | Admin | — | `204 No Content` |

## Event Enrolments

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|---|---|---|---|---|---|
| POST | /api/categories/{categoryId}/enrolments | Enrols the logged-in participant into a category | Participant | `{ }` *(userId taken from auth token)* | `201 Created` — created enrolment object |
| GET | /api/users/me/enrolments | Lists the logged-in participant's enrolments | Participant | — | `200 OK` — array of enrolment objects |
| GET | /api/categories/{categoryId}/enrolments | Lists all enrolments for a category | Admin | — | `200 OK` — array of enrolment objects |
| PUT | /api/enrolments/{id} | Updates enrolment status (e.g. confirm/cancel) | Admin | `{ status }` | `200 OK` — updated enrolment object |
| DELETE | /api/enrolments/{id} | Cancels/withdraws an enrolment | Admin, Participant *(own enrolment only)* | — | `204 No Content` |

## Results

| HTTP Method | Route | Description | Role Required | Request Body | Expected Response |
|---|---|---|---|---|---|
| POST | /api/enrolments/{enrolmentId}/result | Captures a result for a participant's enrolment | Admin | `{ finishTime, position, status }` | `201 Created` — created result object |
| GET | /api/categories/{categoryId}/results | Lists all results for a category (leaderboard) | Admin, Participant | — | `200 OK` — array of result objects |
| GET | /api/users/me/results | Lists the logged-in participant's own results | Participant | — | `200 OK` — array of result objects |
| PUT | /api/results/{id} | Updates/corrects a result | Admin | `{ finishTime, position, status }` | `200 OK` — updated result object |
