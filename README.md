# claude-architecture-patterns-skill

A Claude Code skill for selecting and applying maintainable software architecture patterns in backend and distributed systems.

## Overview

This skill helps developers choose architectural structures that fit the problem rather than copying patterns by habit. It focuses on boundaries, dependency direction, domain modeling, testability, and the trade-offs involved in scaling and evolving a system.

## Main Architecture Approaches

### Clean Architecture

Organize code around business rules and keep infrastructure details outside the core domain. Define clear boundaries between entities, application use cases, interfaces, and adapters.

### Hexagonal Architecture

Separate application logic from external systems through ports and adapters. This makes integrations easier to replace and business logic easier to test.

### Domain-Driven Design

Model the business domain explicitly. Identify bounded contexts, aggregates, entities, value objects, and domain services where they clarify the problem.

### Modular Monoliths and Service Decomposition

Start with cohesive modules and explicit boundaries. Consider service decomposition only when independent deployment, scaling, ownership, or failure isolation justify the added operational cost.

## When to Use This Skill

- Designing a new backend system.
- Refactoring tightly coupled application code.
- Establishing architecture conventions for a team.
- Introducing domain boundaries.
- Improving testability and dependency management.
- Planning service decomposition.
- Reviewing architecture trade-offs.

## Installation

```bash
git clone https://github.com/Brajesh31/claude-architecture-patterns-skill.git ~/.claude/skills/architecture-patterns
```

## Usage

Invoke the skill for architecture planning or review:

```text
/architecture-patterns
```

Provide the business domain, system constraints, expected scale, team structure, deployment model, and current pain points.

## Recommended Workflow

1. Clarify domain boundaries and system responsibilities.
2. Identify functional and non-functional requirements.
3. Map dependencies and data ownership.
4. Select candidate patterns based on actual constraints.
5. Compare complexity, coupling, testability, and operational cost.
6. Define a small implementation boundary.
7. Validate the design with a concrete use case.
8. Document decisions and expected consequences.

## Implementation Playbook

The repository includes `resources/implementation-playbook.md`, which provides practical guidance for applying and reviewing architecture patterns.

## Architecture Checklist

- Business logic is separated from infrastructure concerns.
- Dependencies point in deliberate directions.
- Modules have clear ownership and interfaces.
- Data boundaries are explicit.
- Tests can exercise important logic without unnecessary infrastructure.
- Failure handling and observability are considered.
- Complexity is justified by measurable needs.
- Future change paths are understood.

## Repository Contents

- `SKILL.md`: Main architecture pattern guidance.
- `resources/implementation-playbook.md`: Implementation and review playbook.
- `README.md`: Pattern overview and decision workflow.

## Practical Principle

Do not introduce microservices, event sourcing, or elaborate abstraction layers simply because they are popular. Choose the simplest architecture that satisfies the system's current requirements while leaving reasonable room to evolve.
