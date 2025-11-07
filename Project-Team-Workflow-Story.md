# The Journey of Feature PROJ-123: A Story from Idea to Done

> A narrative to help you feel how real teamwork flows. Follow the characters, notice the steps.

---

## Cast

- Sara (Product Lead): turns needs into stories.
- Omar (Backend Dev): builds APIs.
- Lina (Frontend Dev): builds user interfaces.
- Youssef (QA / Tester): makes sure things really work.
- You (Observer / New team member).

## Day 0: The Problem Appears

Sara says: "Students are emailing assignments as attachments. It's messy. We need an in-portal upload." Everyone nods. She opens Jira and creates an Epic: "Assignment Submission".

Inside the Epic she writes a User Story:

```md
Story PROJ-123: As a student, I want to upload an assignment so that my instructor can grade it easily.
Acceptance Criteria:
- Upload supports PDF and DOCX
- Max file size 10MB; show clear error if bigger
- Success message after upload

```
She leaves it in the Backlog column.


## Day 1: Sprint Planning


Team gathers. Sara explains the story. Omar asks, "Do we need virus scanning now?" Answer: "Not in this version." Lina asks, "Do we show progress bar?" "Optional—defer." The team estimates: 5 story points. It fits in the sprint. Story moves to "Selected for Sprint".

## Day 2: Breaking It Down


Omar and Lina list tasks in Jira under PROJ-123:

- Backend: endpoint `POST /api/v1/assignments` (Omar)
- QA: test cases + edge file sizes (Youssef)

## Day 2 (Afternoon): Work Begins


Omar moves the story to "In Progress" and creates a branch:
```bash

git checkout -b feature/PROJ-123-assignment-upload main
```

He writes a simple controller that just logs "TODO store file" and returns 200. Commits:
```bash
git add .

git commit -m "feat(PROJ-123): scaffold assignment upload endpoint"
```
Pushes and opens a Pull Request (PR) linking PROJ-123.

## Day 3: Parallel Frontend

git checkout -b feature/PROJ-123-upload-form main

```
She doesn't wait for backend; she adds a form that fakes success using a mock function. Commits:

```bash
git commit -m "feat(PROJ-123): add assignment upload form (mocked)"
```

Pushes and opens her PR.

## Day 3 (Late): First Reviews
You open Omar's PR. Checklist:


- Does endpoint name match Acceptance Criteria?
- Any obvious security issue? (No auth yet—flag for later.)
- Code readable? Yes.


git commit -m "chore(PROJ-123): add TODO for size validation"
```
Pushes; PR passes tests; merged into main. Story still "In Progress" because frontend not done.


## Day 4: Integrating Form with Live API
Lina switches her mock call to real fetch:

```js
fetch('/api/v1/assignments', { method: 'POST', body: formData })

```
She handles size check on client before sending. Adds a basic unit test for the size validator. Updates PR and asks Omar: "Server will reject >10MB too?" Omar adds server-side check + returns 413 error with JSON message.

## Day 4 (Later): QA Prepares
Youssef writes test notes:

Test Case 2: 12MB DOCX -> Error: "File too large".

Test Case 3: Unsupported type (.exe) -> Error: "Unsupported file type".
```
He comments these on the story so everyone sees definition of "Done" sharpening.

## Day 5: Frontend PR Review

You and Sara review Lina's PR:
- Upload form clear? Yes.
- Error messages human-friendly? Yes.
- Works on mobile? Quick responsive check passes.

Merge approved. PR merges. Story moves to "In Review" for QA.

## Day 6: QA Verification
Youssef tests on staging (deployed automatically after merge to main). All three cases pass. He finds one edge case: uploading blank file shows generic error. Lina patches it:
```bash
git checkout -b fix/PROJ-123-empty-file-validation main
git commit -m "fix(PROJ-123): add empty file validation"
```
PR merged quickly.

## Day 6 (Afternoon): Story Completion
All acceptance criteria met. Sara moves story to "Done". Velocity updated in Jira charts automatically.

## Day 7: Retrospective Chat
Team reflects:
- Good: Parallel FE/BE saved time.
- Improve: Add API spec earlier to reduce assumptions.
- Action: Next sprint starts with a shared Swagger file for each new endpoint.

## The Invisible Glue (What Made It Work)
- Clear acceptance criteria from start.
- Branch names tied to Jira key.
- Small commits with descriptive messages.
- Early PRs (even before full logic) to invite feedback.
- QA involved before the very end.
- Retrospective action item captured.

## Quick Reference (From the Story)
| Step | Tool | Action | Result |
|------|------|--------|--------|
| Create Story | Jira | Epic + Story + Acceptance Criteria | Shared understanding |
| Start Work | Git/Jira | Move to In Progress + create branch | Traceable progress |
| Early API | Git | Scaffold endpoint + PR | Fast feedback |
| Mock Frontend | Git | Form with placeholder logic | Parallel progress |
| Integrate | Git | Replace mock with real call | Feature emerges |
| Validate | QA/Jira | Test cases posted | Clear definition of done |
| Fix Edge Case | Git | Small fix branch | Quality improved |
| Close Story | Jira | Move to Done | Value delivered |
| Retro | Team | Note improvements | Process evolves |

## Your Turn (Replay This Story)
1. Create a new story: "As an instructor, I want to download submitted assignments so I can review offline." Add 3 acceptance criteria.
2. Backend branch: scaffold `GET /api/v1/assignments/:id/download` returning a dummy file.
3. Frontend branch: add a "Download" button calling that endpoint.
4. Write 2 test cases (success + missing assignment).
5. Merge, test on staging, retrospective note: "Add file type in response headers".

---

Treat each feature like a mini story arc. Clarity at the beginning makes the ending simple.
