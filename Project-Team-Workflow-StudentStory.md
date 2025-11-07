# A Student Team's Journey: Building Together

> A story for students, by students. Follow the team as they learn to work together, use Jira, and ship their first project.

---

## Meet the Team
- **Mona**: Loves design, wants to make the app look great.
- **Ali**: Enjoys coding, always curious about how things work.
- **Sara**: Organized, keeps everyone on track.
- **Omar**: Likes to test and break things (in a good way!).

## The Assignment

Their teacher says: "You need to build a simple assignment submission portal. Students upload files, teachers download and grade."

The team meets in the library. Mona says, "Let’s make it easy to use!" Ali nods, "And secure!" Sara opens her laptop: "Let’s plan in Jira so we don’t forget anything."

## Step 1: Breaking Down the Work

Sara creates a new project in Jira. She adds big tasks (Epics):
- Student uploads assignment
- Teacher downloads assignment

Then, she adds smaller tasks (Stories):
- As a student, I want to upload a PDF or DOCX so my teacher can grade it.
- As a teacher, I want to see a list of submissions.

## Step 2: Assigning Roles

Sara asks, "Who wants frontend?" Mona and Ali raise their hands. Omar says, "I’ll test everything!"

They split into two groups:
- Mona & Ali: Frontend (the website)
- Sara & Omar: Backend (the server and database)

## Step 3: Making a Plan

Sara draws a board on the whiteboard:
- To Do | In Progress | In Review | Done

She moves the first story to "In Progress" and writes everyone’s names next to their tasks.

## Step 4: Creating the Repos

Ali creates two GitHub repos:
- `student-portal-frontend`
- `student-portal-backend`


He invites everyone. Mona says, "Let’s make a branch for each feature!"

## Step 4.5: How We Work Together (Git Flow & Jira)

Sara explains, "Let’s use a simple flow so we don’t get lost!"

**Jira Workflow:**
- Every task starts in "To Do".
- When you start working, move it to "In Progress".
- When you finish your code and open a Pull Request, move it to "In Review".
- After review and testing, move it to "Done".

**Git Flow:**
- Always start a new branch for each feature or fix. Name it like `feature/short-description` or `fix/short-description`.
- When your code is ready, push your branch and open a Pull Request (PR) to `main` (or `develop` if your teacher says so).
- Ask a teammate to review your PR. Fix anything they suggest.
- When everyone is happy, merge your PR. Now your code is part of the project!

Ali says, "So, every new thing we build gets its own branch and its own card in Jira!"
Mona adds, "And we never work directly on `main`—that keeps things safe."
Sara smiles, "And we always know what’s left by looking at the board."

## Step 5: Working on Features

Mona starts a branch:
```bash
git checkout -b feature/upload-form
```
She builds a simple form. Ali helps connect it to the backend.

Sara and Omar work on the backend:
```bash
git checkout -b feature/upload-endpoint
```
They write code to accept files and save them.

## Step 6: Pull Requests and Reviews

When Mona finishes, she opens a Pull Request (PR):
- Title: `feat: add upload form`
- Description: "Lets students upload PDF/DOCX."

Omar reviews it: "Looks good! But what if the file is too big?"
Mona adds a check for file size. Ali tests it and approves.

## Step 7: Testing and Moving Cards

Omar tries to upload a huge file. The app says, "File too large!" He smiles.
Sara moves the card to "Done" in Jira.

## Step 8: Demo Day

The team shows their app to the class. Mona uploads a file, Ali shows the teacher view, Sara explains the workflow, and Omar tries to break it (but can’t!).

The teacher says, "Great teamwork! You used Jira, Git, and code reviews just like real developers."

## What They Learned
- Break big problems into small tasks.
- Use Jira to track progress.
- Make branches for each feature.
- Review each other’s code.
- Test everything!
- Move cards to "Done" when finished.

## Try It Yourself!
1. Make a team of 3–4.
2. Pick a simple project (like a to-do app).
3. Create a Jira board and GitHub repos.
4. Write stories, assign roles, and start coding!
5. Review, test, and demo your work.

---

**Every project is a story. Work together, help each other, and celebrate when you move that last card to Done!**
