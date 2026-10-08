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
