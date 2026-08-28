---
name: grill-me
description: Help developers using coding agents retain solution knowledge by quizzing them on the current codebase one question at a time, grading each response against the implementation, and explaining incorrect answers. Use when a user asks "Do I know this codebase?", "quiz me on this codebase", "grill me", wants to verify or refresh their mental model of a repository, or wants to catch knowledge drift after delegating implementation work to coding agents.
---

# Grill Me

Test the developer's working mental model of the codebase. Prefer questions about behavior, control flow, data flow, state, boundaries, tradeoffs, and failure handling over syntax or trivia.

## Run the quiz

1. Treat the current worktree as authoritative and keep the quiz read-only.

2. Inspect the repository and privately select a substantive file, component, workflow, configuration, or implementation detail that can support a useful question. Exclude generated code, vendored dependencies, and trivial facts such as names or line numbers.

3. Read the selected file or a relevant bounded section. Inspect callers, callees, tests, configuration, and downstream effects when needed to establish the correct answer.

4. Track selected paths and question subjects in the current conversation. Avoid repeating questions until useful subjects are exhausted.

5. Form exactly one focused, self-contained question about how that part of the project works. Prefer mechanism, consequence, rationale, dependencies, workflow, or failure handling.

6. Keep the answer private and wait for the user's response. Do not provide hints unless explicitly requested.

7. Grade the response semantically against the repository. Accept different terminology when the explanation preserves the actual behavior and important consequences.

8. Resolve the question using one of these outcomes:

- If correct, reply:
  `Correct. Would you like another question?`

- If incorrect, begin with:
  `Incorrect.`

  Then concisely explain the actual behavior and reference the relevant local files or components.

  End with:
  `Would you like another question?`

9. If the user continues, select a different useful subject and ask exactly one new question.

10. If the user challenges the grade, re-open the relevant implementation, verify the evidence, and correct the grade if warranted.

## Question quality

- Ask questions useful for understanding and maintaining the project.
- Favor cross-component relationships and observable behavior.
- Match difficulty to the repository's actual contents.
- Never fabricate behavior when information is incomplete.
- Keep each question narrow enough to grade.
- Do not reveal the answer in the question.
- When the repository has too little substantive material for a grounded question, say so instead of inventing one.
