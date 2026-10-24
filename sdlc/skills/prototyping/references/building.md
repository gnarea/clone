# Building a prototype

- Effort MUST go into what the questions depend on. Whatever is already known to work MUST be left out or stubbed.
- Whatever only serves code that has to last (e.g., unit tests, documentation, continuous integration, linting, the conventions of the codebase it's built in) SHOULD be left out.
- In an existing codebase, the prototype MUST be kept apart from the code that ships, so that none of it can ship by accident.
- A path outside the main journeys MAY be left unimplemented. Where one is, it MUST fail immediately and state that the case is unsupported, so that the gap can't be mistaken for a defect.
- The prototype MUST be tested from the outside, in the environment it's meant to run in: an end-user application through what a user would do, a server-side application through what a client would do, and a library through what a consuming application would do. Units MUST NOT be tested individually.
- The tests MUST cover the main journeys and the technical hypotheses, and nothing else.
