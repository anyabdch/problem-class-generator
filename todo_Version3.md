# Project TODO List

## Phase 1: Project Setup and Skeleton
- [ ] Initialize Django project with basic structure.
- [ ] Configure virtual environment and package management.
- [ ] Create Dockerfile and docker-compose for local development.
- [ ] Set up CI configuration and initial unit tests.

## Phase 2: Authentication & User Management
- [ ] Implement Microsoft SSO authentication flow.
- [ ] Create user models and role management.
- [ ] Write tests for SSO login and access control.

## Phase 3: Classroom and Problem Class Management
- [ ] Create endpoints for classroom creation and joining.
- [ ] Develop classroom setting configurations.
- [ ] Build Problem Class model and CRUD endpoints.
- [ ] Build Problem management module with validations.

## Phase 4: LLM Integration for Problem Generation
- [ ] Integrate Anthropic API for batch problem generation.
- [ ] Develop teacher interface for problem review and approval.
- [ ] Set up prompt template management.

## Phase 5: Submission and Grading Infrastructure
- [ ] Implement endpoints for code submission with file validation.
- [ ] Set up Celery grading worker and test suite execution.
- [ ] Develop job status tracking and real-time updates.

## Phase 6: Audit Logging and Security
- [ ] Implement audit logging for critical events.
- [ ] Ensure encryption of sensitive data and secure file handling.
- [ ] Write tests for security and audit log integrity.

## Phase 7: Frontend Integration and End-to-End Testing
- [ ] Develop UI components for all backend modules.
- [ ] Integrate authentication, classroom management, and problem workflows.
- [ ] Write comprehensive end-to-end tests simulating complete user flows.