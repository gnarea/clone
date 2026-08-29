# Testing

## Unit testing

- All **public/exported** functions, procedures, and the like, in every package or module MUST be thoroughly unit tested.
- Tests whose arrange, act, and assert (AAA) blocks overlap substantially MUST be generated dynamically using a data-driven approach (aka _parametised testing_), as long as they test the same unit.
- **Private/internal** functions, procedures, and the like, MUST NOT be unit tested directly. They MUST be tested via the public/exported counterparts that use them instead.
- Real dependencies MUST be preferred over test doubles, including databases and cryptography operations. Where the real thing is used, each test run MUST get its own isolated instance or namespace.
- Test doubles MUST be confined to the I/O boundary and to sources of non-determinism. Mocks and spies MUST NOT be used to make one of our own units testable: a unit that needs them MUST be redesigned instead.
- Where a double is unavoidable, it MUST be a working implementation whose failures are injected explicitly, and whose state is exposed so that tests assert on outcomes rather than on interactions.
- Doubles that consumers of a published library will need MUST ship as part of that library, and MUST be held to the same standards as the rest of it.

## Quality gates

- Coverage MUST be gated in CI at 100% for libraries and server-side applications. A lower bar MAY be set for other artefacts (e.g., a GUI), as long as it's deliberate, per artefact, and written down.
- The only permissible escape valve is excluding files that contain no logic. The threshold MUST NOT be lowered, and any exclusion or relaxation MUST cite the specific bug or platform limitation that forces it.

## Functional testing

- Functional tests MUST exercise the deployed system over the network, and MUST NOT import the code under test.
- They MUST NOT touch backing services directly, and MUST NOT use mocks or spies.
- Where the system ships a client library, the functional tests MUST drive the system through it, so that they double as contract tests for that library.
- The code they exercise MUST NOT count towards unit test coverage.
