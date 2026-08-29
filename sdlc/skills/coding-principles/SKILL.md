---
name: coding-principles
description: Principles and conventions when implementing or reviewing code changes.
---
# Coding principles

## Naming

- All identifiers (e.g., function names) MUST be self-explanatory and concise. Additionally, they SHOULD match the taxonomy of the user and/or programming interfaces.
- Constants, variables, fields, and the like, SHOULD be named after what they hold, rather than what they are used for.
- Functions, procedures, and the like, MUST be written in imperative form (e.g., `submitResult`) or as questions (e.g., `wasResultSubmitted`).

## Code organisation

- (TODO: MVC/etc for partitioning without prescribing a particular paradigm as it'll depend on the nature of the software and tech stack.)
- Files SHOULD NOT span more than 800 LOC, including comments and new lines. 1 kLOC or more SHOULD be deemed a code smell.

## Data model

TODO

## Functions, procedures, and the like

TODO

## Comments

- You MUST NOT add or augment code comments, unless the rationale for a particular block of code could not be inferred by carefully analysing the surrounding code.
- All public or exported members of **published libraries** MUST have appropriate doc comments.
- All comments MUST be succinct and avoid references to specific files/lines in the project.

## Unit testing

- All **public/exported** functions, procedures, and the like, in every package or module MUST be thoroughly unit tested.
- Tests whose arrange, act, and assert (AAA) blocks overlap substantially MUST be generated dynamically using a data-driven approach (aka _parametised testing_), as long as they test the same unit.
- **Private/internal** functions, procedures, and the like, MUST NOT be unit tested directly. They MUST be tested via the public/exported counterparts that use them instead.
