# Leave Management — Coding Standards

## 1. Purpose

This document defines the coding and engineering standards for the Leave Management module.

The purpose of these standards is to keep the codebase consistent, readable, maintainable, testable, and easy for multiple developers to collaborate on.

These standards apply to frontend, backend, API, database, testing, and documentation changes.

---

## 2. General Coding Principles

All code should follow these principles:

- Keep code simple and readable.
- Prefer clear and maintainable solutions.
- Avoid unnecessary complexity.
- Follow the existing project structure.
- Avoid duplicate logic.
- Keep functions and components focused on a single responsibility.
- Validate inputs before processing them.
- Handle errors explicitly.
- Do not hard-code sensitive information.
- Write code that can be tested independently.
- Update documentation when behaviour changes.

---

## 3. Naming Conventions

Names should clearly describe the purpose of the variable, function, component, class, file, or database field.

### General Rules

Use meaningful names instead of short or ambiguous names.

leaveRequest
availableBalance
calculateLeaveDays

## 4. Frontend Naming Standards

The proposed frontend uses React / Next.js.

Components

React components should use PascalCase.

LeaveRequestForm
LeaveStatusCard
ManagerApprovalPanel
EmployeeDashboard

## 5.Variables and Functions

Use camelCase.

leaveRequest
availableBalance
submitLeaveRequest()
calculateLeaveDays()
Boolean Variables

Boolean variables should communicate a true/false meaning.

Good:

isActive
isApproved
hasBalance
canCancel

Avoid:

active
approve
balance
Files

## 6.Component files should use clear component names.

LeaveRequestForm.jsx
LeaveStatusCard.jsx
ManagerApprovalPanel.jsx

The exact file extension should follow the project's selected frontend configuration.

## 7.Backend Naming Standards

The proposed backend uses Python with FastAPI or Django.

Variables and Functions

Use snake_case.

leave_request
available_balance
calculate_leave_days()
validate_leave_request()
Classes

Use PascalCase.

LeaveRequest
LeaveBalance
ApprovalHistory
Constants

Use uppercase with underscores.

MAX_LEAVE_DAYS
DEFAULT_LEAVE_STATUS
Python Files

Use lowercase snake_case.

leave_request.py
leave_service.py
approval_service.py