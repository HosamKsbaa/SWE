# Project Team Workflow: From Jira Issue to Deployed Feature

> A concise, teachable walkthrough for students on how professional teams structure work using Jira, Git, and clear collaboration practices.

## 1. Big Picture Overview

You receive a project goal (e.g., "Build a course management portal"). The team breaks it into business chunks (Epics), smaller user-centric slices (User Stories), and implementable steps (Tasks/Subtasks). Each implementable piece travels a lifecycle: Idea → Jira Issue → Branch → Code → Pull Request → Merge → Deploy → Done.

## 2. Module & Team Structure

- Split the system into logical modules (e.g., `frontend/web`, `backend/api`, `auth`, `data`, `infra`).
- Each module has owners (2 members per FE/BE suggested) responsible for code quality and reviews.
- Clear boundaries reduce merge conflicts and clarify responsibility.

## 3. Repository Strategy

Two common approaches:

- Polyrepo: Separate repos (`frontend` and `backend`). Pros: isolation, simpler tooling per stack. Cons: harder cross-cutting changes.
- Monorepo: One repo with folders (`/apps/frontend`, `/apps/backend`). Pros: single CI pipeline, atomic changes, shared libraries. Cons: more complex tooling configuration.

Pick one and document it early; use consistent naming.

## 4. Jira Concepts & Vocabulary

- Epic: Large feature set ("User Management").
- Story (User Story): Describes value to end user. Format: As a ROLE I want GOAL so that BENEFIT.
- Task: Technical work ("Implement password hashing").
- Subtask: Small unit inside a task ("Add bcrypt dependency").
- Bug: Defect needing fix.
- Sprint: Time-box (usually 1–2 weeks) with a committed scope.
- Board: Visual workflow (To Do → In Progress → Code Review → Done).

## 5. Writing Good User Stories (INVEST)

- Independent, Negotiable, Valuable, Estimable, Small, Testable.

Example: As a student I want to upload assignments so that instructors can grade them.

Add Acceptance Criteria: bullet points describing success conditions.

## 6. Estimation & Planning

- Use Story Points (relative complexity: 1,2,3,5,8,13...).
- During Sprint Planning: select prioritized stories until velocity limit reached.
- Break stories into tasks that can be finished within the sprint.

## 7. Jira Workflow States & Transitions

Typical columns: Backlog → Selected for Sprint → In Progress → In Review → In QA/Test → Done.

Rules:

- Move to In Progress only when you start coding.
- Link branch + PR before moving to In Review.
- "Done" only when merged, tested, and (if required) deployed.

## 8. Branch Naming Conventions

Use structured names to map Git to Jira:

- Feature: `feature/PROJ-123-user-upload`
- Bugfix: `bugfix/PROJ-210-timezone-error`
- Hotfix (production emergency): `hotfix/PROJ-301-null-pointer`
- Release: `release/2025-11-07` or semantic version `release/v1.2.0`

Keep names lowercase with hyphens; include Jira key for traceability.

## 9. Git Flow (Simplified)

Core branches:

- `main` (or `master`): Production-ready. Always deployable.
- `develop`: Integration branch (optional if using trunk-based development).

Supporting branches:

- Feature branches from `develop` (or `main` in trunk-based).
- Release branches from `develop` to stabilize a version.
- Hotfix branches from `main` for urgent fixes.

Lifecycle example (feature):

1. Jira story moves to In Progress.
2. Create branch: `git checkout -b feature/PROJ-123-user-upload main`.
3. Commit small, descriptive changes.
4. Open Pull Request (PR) referencing Jira issue.
5. Reviews + automated tests pass.
6. Merge (squash or rebase) → Jira story to Done.

## 10. Commit Message & PR Guidelines

- Commit message format: `<type>(PROJ-123): short summary`
  - Types: feat, fix, docs, chore, refactor, test.
  - Example: `feat(PROJ-123): add assignment upload endpoint`
- PR checklist:
  - Linked Jira issue
  - Acceptance criteria satisfied
  - Tests added/updated
  - No large unrelated changes
  - Code passes lint & CI

## 11. Feature Lifecycle (End-to-End)

Idea → Grooming (clarify, estimate) → Added to Sprint → Branch created → Code & tests → PR review (peers + automated checks) → Merge → Deploy → Jira Done → Retrospective insights.

## 12. Backend & Frontend Collaboration

- Define API contracts early (OpenAPI / Swagger spec) in a shared location (`/docs/api-spec.yaml`).
- Frontend can mock responses while backend builds endpoints.
- Version APIs: `/v1/users`, `/v2/users` to avoid breaking clients.
- Schedule hand-off syncs (15 mins) for cross-module alignment.

## 13. Dependency & Interface Management

- Use clear package managers (npm+package.json, Maven/Gradle, etc.).
- Lock versions (`package-lock.json`, `pnpm-lock.yaml`, `requirements.txt`).
- Document shared DTOs/types in a common library (e.g., `libs/types`).
- Run automated dependency audit weekly.

## 14. Code Quality & Testing Layers

- Lint (ESLint, Prettier, Checkstyle) enforced in CI.
- Unit tests: logic isolation.
- Integration tests: API + DB.
- End-to-End (E2E): user flows.
- Use coverage thresholds (e.g., 80%).

Fail fast in CI to keep feedback loop short.

## 15. Continuous Integration (CI) & Automation

- Trigger pipeline on PR: install, lint, test, build.
- Optionally add: security scan (SAST), dependency audit, container build.
- Merge blocked until required checks pass.

## 16. Daily Team Rhythm

- Daily Standup: yesterday / today / blockers (keep under 15 mins).
- Async updates in Jira comments when significant change occurs.
- Weekly Sprint Review & Retrospective (what went well, what to improve).

## 17. Example Scenario (Walkthrough)

1. Epic: "Assignment Submission".
2. Story: PROJ-123 As a student I want to upload an assignment so it can be graded.
3. Acceptance Criteria: file types, size limit, success message.
4. Tasks: API endpoint, DB schema change, frontend form component, validation, tests.
5. Branch created: `feature/PROJ-123-upload-endpoint`.
6. Backend implements POST `/api/v1/assignments` + tests.
7. Frontend creates form component using mock API spec.
8. PR opened; reviewers approve; CI green.
9. Merged to `develop`; later part of release branch; deployed to staging; validated; merged to `main`.
10. Jira issue moved to Done.

## 18. Common Pitfalls & How to Avoid Them

- Oversized stories → Split earlier.
- Long-lived branches → Rebase frequently or adopt trunk-based.
- Unlinked PRs → Enforce Jira key in branch name.
- "Done" without tests → Add minimal tests first.
- Hidden work (not in Jira) → Require every code change to reference an issue.

## 19. Glossary (Quick Definitions)

- Trunk-Based Development: Short-lived branches directly off `main`.
- Rebase vs Merge: Rebase rewrites history; merge preserves branch commits.
- CI/CD: Continuous Integration / Continuous Deployment.
- Velocity: Average story points delivered per sprint.

## 20. Quick Reference Cheat Sheets

### Branch Commands

```bash
git checkout -b feature/PROJ-123-user-upload main
git add . && git commit -m "feat(PROJ-123): add upload form"
git push origin feature/PROJ-123-user-upload
```

### Jira Issue Template

```md
Story: As a ROLE I want GOAL so that BENEFIT
Acceptance Criteria:
- [ ] ...
- [ ] ...
Definition of Done:
- Code merged
- Tests pass
- Deployed to ENVIRONMENT
```

### Pull Request Template

```md
Title: feat(PROJ-123): assignment upload endpoint
Linked Issue: PROJ-123
Description: Implements POST /api/v1/assignments with file validation.
Checklist:
- [ ] Tests added
- [ ] Lint passes
- [ ] No secrets committed
- [ ] API spec updated
```

## 21. Teaching Tips

- Walk a live demo: create a Jira story, branch, minimal commit, open PR.
- Have students pair: one writes backend endpoint, other writes frontend integration.
- Run a mini retro after first sprint simulation.

## 22. Next Steps for Students

1. Form teams & assign module ownership.
2. Create Jira project; define workflow columns.
3. Draft initial epics & 6–10 starter stories.
4. Set branching + commit conventions in README.
5. Implement first feature following full lifecycle.

---

Use this document as a scaffold—encourage questions and adapt examples to your specific domain.
