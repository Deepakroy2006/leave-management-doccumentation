# Project Nexelis — Leave Management

> Engineering Design & Documentation Baseline

Leave Management is a role-based system designed to manage the employee leave workflow from request submission and validation through manager approval, rejection, cancellation, and HR visibility.

This repository captures the functional requirements, technical design, API contract, data model, engineering standards, and quality practices established before implementation begins.

The objective is to give the development and QA teams a clear, shared technical baseline before moving into live development.
> Technical Design & Engineering Baseline · Week 1

## 1. Overview

Leave Management is a role-based workflow for managing employee leave from
request submission through approval, rejection, cancellation and record
visibility.

The system is designed around three primary roles:

- **Employee** — submits leave requests and tracks their status.
- **Manager** — reviews assigned requests and approves or rejects them.
- **HR** — accesses organization-level leave records.

The purpose of this repository is to establish the functional understanding,
technical design and engineering standards required before implementation
begins.

---

## 2. Problem Statement

Leave requests should follow a controlled and traceable workflow rather
than being handled as an isolated form submission.

The system needs to ensure that:

- employees can submit valid leave requests;
- leave rules are validated before approval;
- requests reach the appropriate manager;
- managers can approve or reject requests;
- employees can track the resulting status;
- HR can access relevant leave records;
- role-based access is enforced;
- important actions remain traceable.

---

## 3. Leave Workflow

```text
                    ┌─────────────────┐
                    │    Employee     │
                    └────────┬────────┘
                             │
                             │ Submit
                             ▼
                    ┌─────────────────┐
                    │ Leave Request   │
                    │    Validation   │
                    └────────┬────────┘
                             │
                       Valid Request
                             │
                             ▼
                    ┌─────────────────┐
                    │     Pending     │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ Manager Review  │
                    └───────┬─┬───────┘
                            │ │
                   Approve  │ │  Reject
                            │ │
                            ▼ ▼
                       Approved  Rejected
                            │
                            │
                            ▼
                    Employee Status
                            │
                            ▼
                       HR Records