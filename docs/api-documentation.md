# Leave Management — API Draft

## 1. Purpose

This document defines the initial API draft for the Leave Management module.

The API provides the communication layer between the frontend application and
the backend service and supports the core leave request workflow.

The endpoints defined in this document are based on the functional requirements
and represent the proposed API contract for initial implementation.

This document is a design draft. The endpoints will be considered implemented
only after the corresponding backend functionality is developed, tested, and
reviewed.

---

## 2. API Overview

The Leave Management module requires the following initial API endpoints:

| Method | Endpoint | Purpose |
|---|---|---|
| `POST` | `/leave-requests` | Create a new leave request |
| `GET` | `/leave-requests` | Retrieve authorized leave requests |
| `GET` | `/leave-requests/{id}` | Retrieve a specific leave request |
| `PATCH` | `/leave-requests/{id}/approve` | Approve a leave request |
| `PATCH` | `/leave-requests/{id}/reject` | Reject a leave request |

The API follows a REST-based approach where HTTP methods represent the intended
operation on the leave request resource.

---

## 3. Authentication and Authorization

The Leave Management API is intended for authenticated users.

Access to each endpoint must be controlled according to the user's role and
authorization scope.

### Supported Roles

- **Employee** — Can create and track personal leave requests.
- **Manager** — Can review, approve, or reject assigned leave requests.
- **HR** — Can view authorized employee leave records.

Authorization must be enforced by the backend and must not depend only on
frontend controls.

---

# 4. API Endpoints

## 4.1 Create Leave Request

### Method

```http
POST