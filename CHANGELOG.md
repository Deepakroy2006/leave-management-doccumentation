# Leave Management — Changelog

All notable changes to the Leave Management project documentation and
technical baseline are documented in this file.

The format follows a chronological version-based structure so that changes
to requirements, architecture, APIs, database design, and engineering
standards can be tracked clearly.

---

## [Unreleased]

### Added

- Project documentation structure.
- Leave Management project README.
- Functional requirements documentation.
- Technical requirements documentation.
- API documentation draft.
- Database documentation.
- System architecture documentation.
- Coding standards.
- Definition of Done.
- Bug documentation standards.

### Planned

- Implementation of the Leave Management frontend.
- Implementation of backend services.
- PostgreSQL database implementation.
- Authentication and authorization implementation.
- API implementation.
- Automated testing.
- Docker-based development environment.
- CI/CD workflow where applicable.

---

## [0.1.0] — Documentation Baseline

### Added

#### Project Documentation

- Added `README.md`.
- Added project purpose and scope.
- Added user roles and responsibilities.
- Added leave management workflow.
- Added engineering workflow.
- Added project status and documentation guidelines.

#### Functional Requirements

- Added Employee role requirements.
- Added Manager role requirements.
- Added HR role requirements.
- Added leave request workflow.
- Added leave validation requirements.
- Added approval and rejection requirements.
- Added leave status requirements.
- Added cancellation requirements.
- Added functional business rules.
- Added acceptance criteria.

#### Technical Requirements

- Added proposed system architecture.
- Added frontend technology baseline.
- Added backend technology baseline.
- Added REST API requirements.
- Added PostgreSQL database requirements.
- Added authentication and authorization requirements.
- Added validation requirements.
- Added security requirements.
- Added testing requirements.
- Added Docker infrastructure baseline.

#### API Documentation

Added the initial API surface:

| Method | Endpoint | Purpose |
|---|---|---|
| `POST` | `/leave-requests` | Create a leave request |
| `GET` | `/leave-requests` | Retrieve leave requests |
| `GET` | `/leave-requests/{id}` | Retrieve a specific leave request |
| `PATCH` | `/leave-requests/{id}/approve` | Approve a leave request |
| `PATCH` | `/leave-requests/{id}/reject` | Reject a leave request |

#### Database Documentation

Added the proposed database entities:

- Employee
- LeaveRequest
- LeaveType
- LeaveBalance
- ApprovalHistory

Added entity relationships, primary key requirements, foreign key
requirements, data integrity rules, auditability requirements, and
performance considerations.

#### Architecture Documentation

Added:

- Layered system architecture.
- Frontend architecture.
- REST API layer.
- Backend architecture.
- PostgreSQL database layer.
- Docker infrastructure layer.
- Leave request workflow.
- Manager approval workflow.
- Authentication and authorization model.
- Business rule enforcement.
- Error handling.
- Security requirements.
- Testing architecture.
- Scalability considerations.

#### Coding Standards

Added standards for:

- Naming conventions.
- Frontend development.
- Backend development.
- API naming.
- Database naming.
- Validation.
- Business logic.
- Authentication and authorization.
- Error handling.
- Logging.
- Comments and documentation.
- Git branching.
- Commit messages.
- Pull Requests.
- Code reviews.
- Testing.
- Security.
- Dependency management.

#### Definition of Done

Added completion criteria covering:

- Requirements.
- Acceptance criteria.
- Functionality.
- Validation.
- Authorization.
- Testing.
- Security.
- Code quality.
- Documentation.
- Git workflow.
- Pull Requests.
- Code review.
- Bug fixes.
- Release readiness.

#### Bug Documentation

Added:

- Bug lifecycle.
- Bug status definitions.
- Severity levels.
- Priority levels.
- Bug report structure.
- Bug ID convention.
- Reproduction steps.
- Expected and actual results.
- Root cause documentation.
- Fix documentation.
- Verification process.
- Regression testing.
- Bug triage checklist.

---

## Change Management Rules

Changes to project documentation should be recorded in this changelog when
they affect:

- Functional requirements.
- Technical requirements.
- System architecture.
- API contracts.
- Database structure.
- Business rules.
- Security requirements.
- Engineering standards.
- Testing strategy.

Minor formatting or spelling corrections do not require a separate changelog
entry unless they materially affect project documentation.

---

## Versioning Guidelines

Version numbers should follow:

```text
MAJOR.MINOR.PATCH