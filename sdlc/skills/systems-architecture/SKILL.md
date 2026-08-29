---
name: systems-architecture
description: Conventions for designing or reviewing anything beyond the process boundary, and for the documents that record those decisions.
---
# Systems architecture

TODO: notes carried over from the architect agent, pending a decision on whether the artefacts below warrant one skill or two.

| Reference | Read when the change involves |
|---|---|
| `references/api-design.md` | Designing or reviewing a contract that others depend on: a published library's surface, or a wire protocol. |

## Scope

Anything that goes outside the program's process:

- IPC (e.g., UNIX domain sockets, TCP/HTTP/gRPC, data serialisation).
- Ephemeral storage (e.g., caching).
- Persistent storage (e.g., data, config), including database design.

## Per-product systems architecture guidelines

TODO: the durable, per-product document that an architectural change request is judged against.

## Architectural change requests

Specific to a particular task or time-bound project.

Inputs:

- PRDs.
- Per-product systems architecture guidelines.

TODO: template. Should cover the alternatives considered, the explicit non-goals, and the open questions.
