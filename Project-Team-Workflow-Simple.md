# Student-Friendly Guide: From Jira to Done (Step by Step)

This is a simple, real-world workflow your team can follow. Read one section at a time and do the actions.

---

## 1) What is the project?

- A project is a goal (for example: "Build a course portal").
- We split the big goal into small pieces we can finish in a few days.

Why it matters: finishing small pieces often keeps the team moving and happy.

## 2) Who does what (roles)?

- Frontend: builds the screens (what users see).
- Backend: builds the server/API (data and logic).
- You can be in pairs: 2 for frontend, 2 for backend per module.

## 3) Modules = parts of the system

- Example modules: `frontend/web`, `backend/api`, `auth`, `payments`.
- Each module has owners who review code and keep quality high.

## 4) Repositories (where code lives)

- Use two repos to keep things simple for students:
  - One repo for frontend
  - One repo for backend
- Name them clearly, like `course-portal-frontend` and `course-portal-backend`.

## 5) Jira in one minute

- Jira is a tool to track work with cards on a board.
- Board columns show status: To Do → In Progress → In Review → Done.
- Each card is one piece of work.

## 6) Issue types you’ll see

- Epic: a big theme (e.g., "Assignments").
- Story: user value (e.g., "Student uploads assignment").
- Task: technical step (e.g., "Add upload endpoint").
- Bug: fix something broken.

## 7) How to write a good Story

- Template: As a ROLE, I want GOAL so that BENEFIT.
- Example: As a student, I want to upload an assignment so that my instructor can grade it.
- Add 2–4 Acceptance Criteria (clear checks that prove it works).

## 8) Acceptance Criteria (How we know it’s done)

Write short checks like:

- File types allowed: PDF, DOCX
- Max size: 10 MB
- Show success message after upload

## 9) Sprints (short time boxes)

- A sprint is 1–2 weeks.
- The team picks a few stories to finish in that time.
- Keep stories small so they fit.

## 10) Start work: move card, create branch

- In Jira, move your story to In Progress.
- Create a branch from `main` for this story.

```bash
# Example branch name
git checkout -b feature/PROJ-123-assignment-upload main
```

## 11) Branch naming (easy rule)

- `feature/PROJ-123-short-name`
- `bugfix/PROJ-210-login-timeout`
- Include the Jira key (like PROJ-123).

## 12) Make changes and commit small

- Work in small steps and commit often.
- Commit message format: `feat(PROJ-123): short summary`

```bash
git add .
git commit -m "feat(PROJ-123): add upload form"
```

## 13) Push and open a Pull Request (PR)

- Push your branch and open a PR to merge into `main` (or `develop` if your team uses it).
- Link the Jira issue in the PR description.

```bash
git push origin feature/PROJ-123-assignment-upload
```

## 14) Code review: what to look for

- Does it meet the acceptance criteria?
- Is the code simple and clear?
- Are there tests?
- Does it break anything else?

## 15) Testing (super simple view)

- Unit test: test one function/class.
- Integration test: test an endpoint with the database.
- E2E test: test the whole user flow in a browser.

Aim for at least unit tests for new logic.

## 16) CI checks (automation)

- When you open a PR, the pipeline runs:
  - install → lint → test → build
- PR must be green (all checks pass) before merge.

## 17) Merge and move the card to Done

- After review and green checks, merge the PR.
- Move the Jira card to Done.
- If there’s a staging environment, test there before calling it Done.

## 18) Your daily routine

- Standup (15 mins): say what you did, what you’ll do, any blockers.
- Keep Jira updated (move cards, add comments if blocked).
- Pair up when stuck for >20 minutes.

## 19) Common mistakes (and quick fixes)

- Huge stories → Split into smaller stories.
- Long branches → Open PRs early and keep them small.
- Unclear PRs → Add screenshots and link Jira issue.
- "Done" without tests → Add at least 1–2 basic tests.

## 20) Tiny cheat sheet

### Branch commands

```bash
git checkout -b feature/PROJ-123-assignment-upload main
git add . && git commit -m "feat(PROJ-123): add upload form"
git push origin feature/PROJ-123-assignment-upload
```

### Jira story template

```md
Story: As a ROLE, I want GOAL so that BENEFIT
Acceptance Criteria:
- [ ] condition 1
- [ ] condition 2
Definition of Done:
- Code merged
- Tests pass
- Deployed to ENV (if required)
```

### Pull request checklist

```md
- [ ] Linked Jira issue (PROJ-123)
- [ ] Meets acceptance criteria
- [ ] Tests added/updated
- [ ] Lint & CI checks pass
- [ ] API/spec/docs updated if needed
```

## 21) First practice assignment (do this)

- Create a Jira story: "Student uploads assignment" with 3 acceptance criteria.
- Create a feature branch from `main` using the naming rule.
- Backend: add a dummy POST `/api/v1/assignments` that returns 200.
- Frontend: add a form with file input and a fake submit.
- Open a PR that links the story and add 1 unit test (FE or BE).

---

Tip: Keep it boring and consistent. Small stories, small PRs, green checks. That’s how real teams ship fast.
