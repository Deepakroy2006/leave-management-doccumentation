# Leave Management — Architecture Diagram

## 1. Purpose

This document provides a visual representation of the proposed
Leave Management system architecture.

It shows how users interact with the frontend, how requests move
through the API and backend, how data is stored in PostgreSQL, and
how the application is supported by infrastructure.

This is a proposed architecture for the documentation baseline.
It does not represent an implemented production system.

---

## 2. High-Level Architecture

+----------------------+
|        Users         |
|----------------------|
| Employee             |
| Manager              |
| HR                   |
+----------+-----------+
           |
           | HTTPS
           v
+----------------------+
|      Frontend        |
|----------------------|
| React / Next.js      |
|                      |
| - Login              |
| - Leave Request      |
| - Leave Status       |
| - Manager Review     |
| - HR Records         |
+----------+-----------+
           |
           | REST API
           v
+----------------------+
|       Backend        |
|----------------------|
| Python               |
| FastAPI / Django     |
|                      |
| - Authentication     |
| - Authorization      |
| - Validation         |
| - Business Rules     |
| - Leave Workflow     |
| - Audit Handling     |
+----------+-----------+
           |
           | SQL
           v
+----------------------+
|      PostgreSQL      |
|----------------------|
| Employee             |
| LeaveRequest         |
| LeaveType            |
| LeaveBalance         |
| ApprovalHistory      |
+----------------------+

           ^
           |
           |
+----------+-----------+
|    Infrastructure    |
|----------------------|
| Docker               |
| Environment Config   |
| Application Runtime  |
| Network              |
+----------------------+

## 3. Request Flow

A typical leave request follows this flow:

Employee
   |
   | Submit Leave Request
   v
Frontend
   |
   | POST /leave-requests
   v
REST API
   |
   v
Backend
   |
   +--> Authenticate User
   |
   +--> Authorize Employee
   |
   +--> Validate Request
   |
   +--> Check Leave Balance
   |
   +--> Check Date Rules
   |
   +--> Check Overlap
   |
   +--> Create Request
   |
   v
PostgreSQL
   |
   | Leave Request Created
   v
Pending Status

 ## 4. Manager Approval Flow
Manager
   |
   | View Pending Requests
   v
Frontend
   |
   | GET /leave-requests
   v
Backend
   |
   +--> Authenticate Manager
   |
   +--> Verify Authorization
   |
   +--> Retrieve Assigned Requests
   |
   v
PostgreSQL
   |
   | Pending Leave Request
   v
Manager
   |
   +-------------------+
   |                   |
   | Approve           | Reject
   v                   v
PATCH /approve     PATCH /reject
   |                   |
   +---------+---------+
             |
             v
          Backend
             |
             +--> Validate Decision
             |
             +--> Prevent Self-Approval
             |
             +--> Update Status
             |
             +--> Create Approval History
             |
             v
         PostgreSQL
             |
             v
      Approved / Rejected
 ## 5. Leave Request Lifecycle
             +---------+
             | Pending |
             +----+----+
                  |
          +-------+-------+
          |               |
          v               v
     +---------+     +----------+
     | Approved|     | Rejected |
     +----+----+     +----------+
          |
          |
          v
   +----------------+
   | Cancellation   |
   | if permitted   |
   +----------------+
          |
          v
     +----------+
     | Cancelled|
     +----------+

The exact cancellation rules depend on the request status and
applicable business rules.

## 6. API Architecture

The initial API surface is:

                    REST API
                       |
       +---------------+---------------+
       |               |               |
       v               v               v
POST /leave-requests   GET /leave-requests
       |
       v
GET /leave-requests/{id}
       |
       +-----------------------+
       |                       |
       v                       v
PATCH /leave-requests/{id}/approve
PATCH /leave-requests/{id}/reject


## 7. Database Architecture

The proposed database model is:

+----------------+
|   Employee     |
+-------+--------+
        |
        | 1 : Many
        |
        +----------------------+
        |                      |
        v                      v
+---------------+      +---------------+
| LeaveRequest  |      | LeaveBalance  |
+-------+-------+      +-------+-------+
        |                      |
        |                      |
        | Many : 1             | Many : 1
        |                      |
        v                      v
+---------------+      +---------------+
|   LeaveType   |      |   LeaveType   |
+---------------+      +---------------+

LeaveRequest
      |
      | 1 : Many
      v
+-------------------+
| ApprovalHistory   |
+-------------------+
## 8. Authentication and Authorization

Authentication and authorization are applied before protected
operations are performed.

Request
   |
   v
+--------------------+
| Authentication     |
+---------+----------+
          |
          | Valid
          v
+--------------------+
| Authorization      |
+---------+----------+
          |
          | Authorized
          v
+--------------------+
| Business Logic     |
+---------+----------+
          |
          v
       Database

Role responsibilities:

Employee
   |
   +--> Create own leave request
   +--> View own leave requests
   +--> Cancel eligible request

Manager
   |
   +--> View assigned requests
   +--> Approve requests
   +--> Reject requests
   +--> Cannot approve own leave

HR
   |
   +--> View leave records
   +--> Perform permitted administrative actions
## 9. Business Rule Enforcement

Business rules are enforced in the backend rather than relying only
on frontend validation.

                    Leave Request
                          |
                          v
                 +----------------+
                 | Required Fields|
                 +-------+--------+
                         |
                         v
                 +----------------+
                 | Date Validation|
                 +-------+--------+
                         |
                         v
                 +----------------+
                 | Leave Balance  |
                 +-------+--------+
                         |
                         v
                 +----------------+
                 | Overlap Check  |
                 +-------+--------+
                         |
                         v
                 +----------------+
                 | Leave Type     |
                 | Rules          |
                 +-------+--------+
                         |
                         v
                 +----------------+
                 | Employee Status|
                 +-------+--------+
                         |
                         v
                 +----------------+
                 | Create / Reject|
                 +----------------+
## 10. Audit Flow

Important workflow actions should be traceable.

User Action
    |
    v
Backend
    |
    +--> Update LeaveRequest
    |
    +--> Record ApprovalHistory
              |
              +--> Action
              +--> Performed By
              +--> Previous Status
              +--> New Status
              +--> Comment
              +--> Timestamp