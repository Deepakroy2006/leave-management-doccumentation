# Leave Management — Database Documentation

## 5. Database Entities


## 1. Purpose

This document defines the proposed database entities and relationships for
the Leave Management module.

The database design supports the complete leave workflow, including employee
leave requests, leave types, leave balances, manager decisions, and approval
history.

The design is based on the functional and technical requirements defined for
the module.

This document represents the proposed database design and is not an
implementation of the production database.

---

## 2. Database Entities

The Leave Management module consists of five core entities:

1. `Employee`
2. `LeaveRequest`
3. `LeaveType`
4. `LeaveBalance`
5. `ApprovalHistory`

These entities work together to support the complete leave request lifecycle.


Employee
   │
   ├──────────────► LeaveRequest ◄────────────── LeaveType
   │                     │
   │                     ▼
   │              ApprovalHistory
   │
   └──────────────► LeaveBalance ◄────────────── LeaveType

### 5.1 Employee

The `Employee` entity stores information about employees who use the
Leave Management system.

| Field | Type | Description |
|---|---|---|
| `id` | Integer | Unique employee identifier |
| `name` | String | Full name of the employee |
| `email` | String | Employee email address |
| `role` | String | Employee, Manager, or HR |
| `manager_id` | Integer | Reference to the employee's manager |
| `status` | String | Current employee status |
| `created_at` | Timestamp | Record creation time |
| `updated_at` | Timestamp | Last update time |

### 5.2 LeaveRequest

The `LeaveRequest` entity stores leave applications submitted by employees.

| Field | Type | Description |
|---|---|---|
| `id` | Integer | Unique leave request identifier |
| `employee_id` | Integer | Employee who submitted the request |
| `leave_type_id` | Integer | Type of leave requested |
| `start_date` | Date | Start date of leave |
| `end_date` | Date | End date of leave |
| `reason` | String | Reason for the leave |
| `status` | String | Pending, Approved, Rejected, or Cancelled |
| `created_at` | Timestamp | Request creation time |
| `updated_at` | Timestamp | Last update time |

### 5.3 LeaveType

The `LeaveType` entity defines the different types of leave available.

| Field | Type | Description |
|---|---|---|
| `id` | Integer | Unique leave type identifier |
| `name` | String | Name of the leave type |
| `description` | String | Description of the leave type |
| `is_active` | Boolean | Indicates whether the leave type is active |
| `created_at` | Timestamp | Record creation time |
| `updated_at` | Timestamp | Last update time |

### 5.4 LeaveBalance

The `LeaveBalance` entity stores the leave allocation and remaining balance
for an employee.

| Field | Type | Description |
|---|---|---|
| `id` | Integer | Unique balance identifier |
| `employee_id` | Integer | Employee associated with the balance |
| `leave_type_id` | Integer | Leave type associated with the balance |
| `total_balance` | Decimal | Total allocated leave |
| `used_balance` | Decimal | Leave already used |
| `available_balance` | Decimal | Remaining leave balance |
| `updated_at` | Timestamp | Last balance update time |

### 5.5 ApprovalHistory

The `ApprovalHistory` entity records actions performed during the leave
approval workflow.

| Field | Type | Description |
|---|---|---|
| `id` | Integer | Unique history record identifier |
| `leave_request_id` | Integer | Related leave request |
| `performed_by` | Integer | Employee who performed the action |
| `action` | String | Approved, Rejected, or Cancelled |
| `previous_status` | String | Status before the action |
| `new_status` | String | Status after the action |
| `comment` | String | Optional action comment |
| `created_at` | Timestamp | Time when the action occurred |