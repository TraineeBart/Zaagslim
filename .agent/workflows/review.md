---
description: Adversarial Code Review Checklist
---

# Workflow: Code Review

Use this to review code (yours or others).

## The Checklist

### 1. Correctness
- [ ] Does it meet the User Scenarios (Given/When/Then)?
- [ ] Are edge cases handled (Nulls, Empty Lists, Network Errors)?
- [ ] Is it thread-safe (if applicable)?

### 2. Quality (The Law)
- [ ] **Type Hints**: Are they complete?
- [ ] **Docstrings**: Are they descriptive?
- [ ] **Complexity**: Are functions < 30 lines? Files < 300 lines?
- [ ] **Naming**: Do names reveal intent? (`d` vs `days_since_active`)

### 3. Architecture
- [ ] **Separation**: Does logic leak into the API layer?
- [ ] **Dependency**: Are imports flowing down?

### 4. Tests
- [ ] Do tests cover the *why*, not just the *what*?
- [ ] Is coverage > 90% for new business logic?

## Verdict
*   **Approve**: Ready to merge.
*   **Request Changes**: List specific violations of "The Law".
