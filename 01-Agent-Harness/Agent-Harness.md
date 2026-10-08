Absolutely bro. Based on the **Agent Harness** concept, here’s a practical **6-file starter harness** you can drop into a vibe-coding project.

The goal is simple: **give the agent the context, rules, memory, tasks, skills, and workflow it needs to work consistently.**


---


# 01 — `PRD.md`


```md
# Product Requirements Document


## 1. Product
Name: [PROJECT NAME]


## 2. Problem
What problem are we solving?


[Describe the problem in 2–4 sentences.]


## 3. Target Users
Who is this for?


- [User type 1]
- [User type 2]


## 4. Core Goal
What should the product help users accomplish?


[One clear sentence.]


## 5. Core Features


### Feature 1 — [NAME]
- What it does:
- User flow:
- Expected result:


### Feature 2 — [NAME]
- What it does:
- User flow:
- Expected result:


## 6. Non-Goals


Do NOT build:


- [Feature]
- [Feature]
- [Feature]


## 7. Success Criteria


The product is successful when:


- [Criteria 1]
- [Criteria 2]
- [Criteria 3]
```


---


# 02 — `RULES.md`


This is probably the **most important file**.


```md
# Project Rules


## General


- Read relevant files before making changes.
- Do not modify unrelated files.
- Prefer simple solutions over abstractions.
- Do not add dependencies unless necessary.
- Never invent APIs, functions, or requirements.


## Code


- Follow the existing project structure.
- Reuse existing components before creating new ones.
- Keep functions small and focused.
- Handle errors explicitly.
- Remove unused code after changes.


## UI


- Follow the existing design system.
- Reuse existing components and styles.
- Do not introduce random colors, fonts, or spacing.
- Make responsive behavior explicit.


## Database


- Never change the schema without checking existing migrations.
- Never delete production data.
- Use migrations for schema changes.


## Testing


Before declaring a task complete:


1. Run the relevant tests.
2. Check for TypeScript/build errors.
3. Verify the affected flow manually when possible.


## Git


- Keep commits focused.
- Do not rewrite history unless explicitly requested.
- Never commit secrets or `.env` files.


## Important


If requirements are unclear:


STOP.


Ask before making a major architectural decision.
```


---


# 03 — `MEMORY.md`


This prevents the agent from repeatedly forgetting project decisions.


```md
# Project Memory


## Architecture


Frontend:
- [Framework]
- [Language]


Backend:
- [Framework]
- [Language]


Database:
- [Database]


Deployment:
- [Platform]


## Important Decisions


### Decision 1
Date: [DATE]


Decision:
[What was decided]


Reason:
[Why]


Do not change unless:
[Condition]


### Decision 2
Date: [DATE]


Decision:
[What was decided]


## Current Constraints


- [Constraint]
- [Constraint]
- [Constraint]


## Known Problems


- [Problem]
- [Problem]


## Things We Tried


### [Approach]
Result:
[What happened]


Do not repeat because:
[Reason]
```


---


# 04 — `TASKS.md`


This keeps the agent from randomly deciding what to build next.


```md
# Tasks


## Current Goal


[What are we trying to accomplish right now?]


## In Progress


- [ ] Task 1
- [ ] Task 2


## Next


- [ ] Task 3
- [ ] Task 4


## Completed


- [x] Task 5
- [x] Task 6


## Task Details


### Task 1
Goal:
[What needs to happen]


Files:
- `src/...`
- `src/...`


Acceptance Criteria:


- [ ] Requirement 1
- [ ] Requirement 2
- [ ] Requirement 3


Do Not:


- [Thing]
- [Thing]


## Definition of Done


A task is complete only when:


- Implementation works
- Tests pass
- No unrelated files changed
- No known errors remain
```


---


# 05 — `SKILLS.md`


Tell the agent **how you expect it to perform recurring types of work.**


```md
# Agent Skills


## Feature Development


When building a feature:


1. Understand the existing architecture.
2. Find reusable components.
3. Identify affected files.
4. Implement the smallest working solution.
5. Test the feature.
6. Review the diff.


## Debugging


When fixing a bug:


1. Reproduce the issue.
2. Identify the root cause.
3. Avoid changing unrelated code.
4. Apply the smallest fix.
5. Test the original failure case.
6. Check for regressions.


## Refactoring


Before refactoring:


- Confirm the current behavior.
- Identify all usages.
- Preserve existing functionality.
- Avoid unnecessary abstractions.


## Code Review


Check:


- Correctness
- Security
- Performance
- Error handling
- Maintainability
- Tests
- Unnecessary complexity
```


---


# 06 — `WORKFLOWS.md`


This is the **agent loop**.


```md
# Agent Workflows


## Feature Workflow


UNDERSTAND
↓
PLAN
↓
IMPLEMENT
↓
TEST
↓
REVIEW
↓
SHIP


## 1. Understand


Before coding:


- Read PRD.md
- Read RULES.md
- Read relevant MEMORY.md sections
- Inspect the existing implementation


## 2. Plan


Create a short implementation plan.


Identify:


- Files to change
- Files to create
- Dependencies
- Risks


## 3. Implement


- Make the smallest reasonable change.
- Follow RULES.md.
- Reuse existing code.


## 4. Test


Run:


- Unit tests
- Type checks
- Build
- Relevant manual checks


## 5. Review


Ask:


- Did I solve the actual problem?
- Did I change anything unnecessary?
- Did I introduce technical debt?
- Did I break existing behavior?


## 6. Ship


Only mark the task complete when:


- Tests pass
- Build passes
- Acceptance criteria are satisfied
- Changes are reviewed
```


---


## The actual harness


The six files work together like this:


```text
                 PRD.md
              WHAT TO BUILD
                   ↓
              TASKS.md
             WHAT TO DO
                   ↓
RULES.md ───→  AGENT  ←─── MEMORY.md
HOW TO WORK       ↓          WHAT TO REMEMBER
                   ↓
              SKILLS.md
             HOW TO EXECUTE
                   ↓
            WORKFLOWS.md
             HOW TO LOOP
                   ↓
                OUTPUT
```


### If you want the minimum version


Start with just:


```text
PRD.md
RULES.md
TASKS.md
```


Then add:


```text
MEMORY.md
SKILLS.md
WORKFLOWS.md
```


as the project becomes more complex.


**One important distinction:** these filenames are a **practical harness template**, not a universal industry-standard six-file specification. Different coding agents use their own native files (`AGENTS.md`, `CLAUDE.md`, skills directories, etc.). The principle is what matters: **context + constraints + memory + execution loop + tools.**
