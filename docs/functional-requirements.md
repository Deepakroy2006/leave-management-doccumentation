# Leave Management — Functional Requirements

## 1. Purpose

This document defines the functional requirements for the Leave Management
module and establishes the expected behaviour of the system from a business
and user perspective.

The requirements provide a common reference for product, development, and QA
teams and serve as the functional baseline for implementation.

This document defines **what the system must do** and the business rules it
must enforce. API contracts, data structures, architecture, and other
implementation details are maintained in the corresponding technical
documentation.

---

## 2. Business Context

The Leave Management module provides a controlled workflow for employees to
request leave, managers to review requests, and HR to access leave records.

The system must support the complete request lifecycle:

```text
Employee
    │
    ▼
Submit Leave Request
    │
    ▼
Validate Request
    │
    ▼
Pending
    │
    ▼
Manager Review
    │
    ├───────────────┐
    ▼               ▼
Approved         Rejected
    │               │
    └───────┬───────┘
            ▼
     Employee Status
            │
            ▼
       HR Visibility