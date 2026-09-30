# Synchronous messaging

Request-response is the exception, for exchanges that can't be made asynchronous.

## When to use it

- Request-response MUST be limited to operations that complete within seconds. Anything slower, or anything that must survive the other party being down, MUST be handed to a broker, and the request acknowledged as accepted (e.g., `202 Accepted`).
- It MUST run over a standard protocol (e.g., HTTP, WebSocket, or gRPC), so that off-the-shelf load balancers and proxies can front it.
- A stream (e.g., a WebSocket or a gRPC stream) MUST be used only where the server pushes to the client. One-shot operations MUST be plain requests.
- A mobile client MUST NOT hold a connection open or poll in the background. The server SHOULD wake it (e.g., with a push notification), and the client then pulls.

## Status codes

- The status code MUST tell the client whether to retry: 4xx means the same request will never succeed, 5xx means it may succeed later, and 2xx means it succeeded or was deliberately dropped.
- A 4xx MUST mean the caller is at fault, and a 5xx that we or our infrastructure are. A failed upstream dependency MUST be reported as `503 Service Unavailable`.
- A 5xx response MUST NOT reveal anything about the server's internals.

## The client

- Every request MUST have a short, explicit timeout, measured in seconds, that the caller can override. A client's timeout MUST be shorter than that of whoever called it.
- Only a 5xx, a timeout, or a lost connection MAY be retried. Retries MUST follow the retry policy in `SKILL.md`, and MUST be capped by the message's expiry, where it has one.
- A client MUST honour `429 Too Many Requests` and `Retry-After`, because retrying blindly deepens the outage it's retrying against.
- A client that calls the same dependency repeatedly SHOULD stop calling it after consecutive failures, and probe it at intervals until it recovers (aka _circuit breaking_), so that a struggling dependency isn't overwhelmed and callers fail fast.
- A client library MUST leave retries to its caller. Instead, the type of each error it raises MUST tell the caller whether retrying could help.

## The server

- An operation that isn't safe (e.g., `POST`) MUST be idempotent, through a natural or client-supplied identifier and a uniqueness constraint, rather than an idempotency key.
- A client that the server doesn't need to identify MUST NOT be required to authenticate. Abusive clients MUST be throttled instead.
- Where a client must authenticate, the request MUST carry a short-lived credential bound to the exact endpoint (e.g., a JWT whose audience is the request URL), and the server MUST NOT keep a session.
- Rate limits MUST apply per client identity as well as per IP address, because one attacker can spread their requests across many addresses (e.g., through residential proxies).
- The number of instances MUST be capped, so that an attack can't scale the bill without bound.

## Long-lived connections

- The server MUST ping the client at a fixed interval, and each side MUST drop the connection once it has missed pings for longer than it expected to, with the client giving up sooner than the server.
- Each reason to close MUST have its own close code, including one that tells the client to reconnect immediately. A connection that closes before the operation is complete MUST close with an error, so that the client doesn't assume the operation succeeded.
- Each item received MUST be acknowledged explicitly, and only once it's durably stored. The number of unacknowledged items in flight MUST be capped.
- An item that can never be processed MUST be acknowledged and dropped, so that it can't block the stream.
