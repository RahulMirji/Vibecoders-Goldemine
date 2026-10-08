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
