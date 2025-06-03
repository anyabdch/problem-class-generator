# Project Blueprint: Automated Problem-Grading and Management Platform

This plan outlines a step-by-step blueprint to build a web application for classroom management, problem generation, automated grading, and mastery-based progression. The architecture is designed for incremental progress using test-driven development (TDD) and best practices. The plan is divided into several major modules, each further decomposed into small, testable steps. Each prompt will build on the previous work to ensure smooth integration.

---

## Overview

The project is a web application that allows teachers to create/manage classrooms, define problem classes and problems, integrate with an LLM (Anthropic) for batch problem generation, and automatically grade student submissions. Key components include:

1. **Authentication & User Management**
   - Support Microsoft SSO via Northwestern accounts.
   - Role-based access control: Teacher, Co-Teacher/TA, and Student.

2. **Classroom & Problem Class Management**
   - Classroom creation and joining with access codes.
   - Define problem classes with attributes (title, description, difficulty, prerequisites, etc.).
   - Define problems with problem statements, test cases, starter code, etc.

3. **LLM Integration for Problem Generation**
   - Integration with Anthropic API to generate problems in batches.
   - Interface for teachers to review, edit, and approve LLM-generated problems.

4. **Submission, Grading, and Mastery**
   - Allow students to submit code files.
   - Automated grading using a test suite.
   - Mastery tracking for progression based on test results.

5. **Backend Infrastructure**
   - API built with Django (Python).
   - Containerized deployment (AWS ECS).
   - Database: MySQL (AWS RDS).
   - File storage: AWS S3 for temporary uploads.
   - Job queue for grading (Celery with Redis/SQS).
   - Audit logging for critical events.

6. **Frontend Requirements**
   - Responsive UI for classroom creation, problem management, submission upload, and result display.

---

## Step-by-Step Blueprint

### Phase 1: Project Setup and Skeleton
1. **Initialize Repository and Basic Setup**
   - Set up the version control structure.
   - Create a new Django project.
   - Set up project directories and configuration files.
   - Write initial unit tests and continuous integration (CI) configuration.

2. **Setup Virtual Environment and Package Management**
   - Configure Virtualenv/Pipenv.
   - Define requirements with a focus on Django, testing frameworks (pytest, Django TestCase), and Celery.

3. **Set Up Docker Environment**
   - Create Dockerfile and docker-compose for local development.
   - Ensure database (MySQL) and Redis (or SQS emulator) are accessible for testing.

### Phase 2: Authentication & User Management Module
1. **Implement Microsoft SSO Integration**
   - Create authentication flow (redirects, callback handlers).
   - Handle user creation and role assignment upon successful SSO.
   - Write tests simulating SSO logins.

2. **Define User Roles and Permissions**
   - Create models for roles (Teacher, TA, Student).
   - Implement role-based middleware.
   - Write tests verifying access control.

### Phase 3: Classroom and Problem Class Management
1. **Classroom Module**
   - Develop endpoints and views for classroom creation, joining via access codes.
   - Implement classroom settings (allowed file types, naming conventions, etc.).
   - Write unit and integration tests.

2. **Problem Class Module**
   - Define models for ProblemClass with attributes: title, description, difficulty, etc.
   - Create endpoints for CRUD operations on Problem Classes.
   - Write tests including validations (e.g., unique titles, max limit per teacher).

3. **Problem Management**
   - Design models for Problems with required test cases.
   - Build creation, review, and approval workflows.
   - Develop endpoints with full TDD coverage.

### Phase 4: LLM Generation Integration
1. **LLM Batch Problem Generation**
   - Integrate with Anthropic API for problem generation.
   - Create teacher interface to initiate batch generation.
   - Implement functionality for editing and approving generated problems.
   - Write tests for API key handling, batch limits, and review process.

2. **Prompt Template Management**
   - Develop a system to store and modify default prompt templates.
   - Test prompt template updates and their usage in generation requests.

### Phase 5: Submission and Grading Infrastructure
1. **Submission Endpoint and File Handling**
   - Create endpoints to accept student submissions.
   - Implement file type checking based on classroom settings.
   - Write tests for file upload consistency and deletion after processing.

2. **Automated Grading Engine**
   - Set up a grading worker using Celery.
   - Design test suites per problem.
   - Write tests to simulate grading, including pass/fail conditions and response times.
   - Integrate grading results with student submission history.

3. **Job Status and Real-Time Feedback**
   - Develop status tracking for grading jobs (queued, grading, completed, error).
   - Implement real-time job status updates for student views.
   - Write tests for status transitions.

### Phase 6: Audit Logging and Security
1. **Logging Infrastructure**
   - Implement comprehensive audit logs for critical events.
   - Ensure logs capture user ID, timestamp, IP address, action, and affected resource.
   - Write tests to verify audit trail consistency and immutability.

2. **Security Enhancements**
   - Encrypt sensitive data (LLM API keys) in the database.
   - Validate file uploads for potential security issues.
   - Conduct tests for access control and log integrity.

### Phase 7: Frontend Development and Integration
1. **UI for Backend Features**
   - Create responsive design for classroom management, submission uploads, and grading status.
   - Build forms and views for user authentication and role management.
   - Use test-driven front-end development practices (e.g., Jest, Cypress).

2. **Wiring and End-to-End Integration Testing**
   - Integrate all backend endpoints with the frontend.
   - Ensure smooth workflow from authentication to problem submission and grading.
   - Develop comprehensive end-to-end tests simulating user flows.

---

## Iterative Chunks and Prompts for Code-Generation LLM

Below are the 8 prompt sections that break the work into small, incremental tasks. Each prompt builds on previous stages and ensures that the integrated solution is fully tested and maintainable.

### Prompt Section 1: Create Project Skeleton

```
Please initialize a new Django project for the Automated Problem-Grading Platform. Include a basic project structure with a README, virtual environment configuration, and initial CI configuration for testing. Write tests using Django's testing framework to ensure the project loads correctly. Also, include a Dockerfile and docker-compose.yml for local development with MySQL and Redis
```

---

### Prompt Section 2: Implement Authentication via Microsoft SSO

```
Build the authentication module using Microsoft SSO integration. Implement the redirect flow, callback handler, and user creation logic. Create unit tests to simulate SSO login and verify role assignment. Ensure that after SSO login, users are created with a default role. Integrate the logic into the existing Django project structure from the previous prompt.
```

---

### Prompt Section 3: Develop Classroom Creation and Joining

```
Develop the Classroom module, including endpoints for creating a classroom by a teacher and joining a classroom via an access code by a student. Ensure that classroom settings (allowed file types, naming conventions) are configurable. Write tests to verify classroom creation, join logic, and configuration validations. Integrate these endpoints securely into the existing project.
```

---

### Prompt Section 4: Build Problem Class and Problem Management Modules

```
Create models and views for Problem Classes which include attributes like title, description, difficulty, prerequisites, and tags. Implement CRUD operations and validations (such as unique titles and a maximum limit per teacher). Additionally, build the Problem management module to support a problem statement, test cases, and optional starter code. Write unit tests to confirm CRUD operations and validation rules. Integrate these modules with the Classroom module so that problems belong within a classroom context.
```

---

### Prompt Section 5: Integrate LLM Batch Generation for Problems

```
Integrate Anthropic API for LLM-based problem generation. Develop an endpoint for teachers to request a batch generation of problems, limiting requests per teacher as required. Implement editing and approval functionality for the generated problems. Write tests for API integration, batch limits, and review workflow. Ensure that this module builds upon the Problem management module with proper interfacing.
```

---

### Prompt Section 6: Implement Submission and Grading Functionality

```
Develop endpoints for student code submissions, enforcing file type restrictions based on classroom settings. Implement a background worker using Celery to grade submissions against test cases. Create a status tracking system for job states (queued, grading, completed, error) and integrate real-time feedback visibility. Write tests for submission file handling, deletion post-grading, and grading result accuracy. Wire this module to the Problem Management module for end-to-end functionality.
```

---

### Prompt Section 7: Build Audit Logging and Security Enhancements

```
Implement audit logging to capture user actions such as logins, classroom and problem modifications, submission events, and grading updates. Ensure logs include user ID, timestamp, IP, action, and resource details, and that they are immutable. Enhance security by encrypting sensitive data like API keys and validating file uploads. Write tests to verify the audit logs and security mechanisms, ensuring they integrate with previous modules.
```

---

### Prompt Section 8: Final Integration and End-to-End Testing

```
Integrate all modules (authentication, classroom management, problem management, LLM integration, submission and grading, audit logging) into a cohesive application. Develop comprehensive end-to-end tests that simulate the user workflow, from logging in with SSO to classroom setup, problem submission, grading, and review. Ensure UI components work with the backend APIs and that data flows securely between modules.
```


---

## Summary

This blueprint breaks the project into a series of small, iterative steps that emphasize test-driven development, security, and incremental integration. Each prompt builds on the previous modules, ensuring there is no hanging or orphaned code. The provided iterative chunks and prompt sections are designed for a code-generation LLM to implement the project in a test-driven manner with continuous integration, ensuring best practices and early testing at every stage.





