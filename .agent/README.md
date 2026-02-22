# Agentic Protocol 2.0

This directory contains the "Brain" of the AI Agent. It is structured according to Anthropic's best practices (Chain of Thought, Few-Shot Context).

## Structure

### 1. The Constitution (`rules/`)
Non-negotiable constraints.
*   `roles.md`: The Persona (Lead Developer).
*   `standards.md`: The Law (Code quality).
*   `documentation.md`: The Memory Protocol.

### 2. The Tracks (`workflows/`)
Step-by-step reasoning guides (Chain of Thought).
*   `new-feature.md`: Thinking -> Planning -> Execution -> Review.
*   `bugfix.md`: The Scientific Method.
*   `review.md`: Adversarial Checklist.

### 3. The Engine (`skills/`)
Knowledge bases with canonical examples (Few-Shot).
*   `api-design`: RestAPI patterns.
*   `python-coding-standard`: Code style.
*   `testing-standard`: Pytest fixtures and patterns.
*   `git-version-control`: Commit and merge rules.

## Usage
The agent MUST consult these files before starting any task to ensure alignment with the "Gold Standard".
