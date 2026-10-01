# Asynchronous messaging

## Delivery

- The processing of a message MUST be idempotent, because the same message can be delivered more than once (e.g., when its acknowledgement is lost).
- Consumers MUST NOT depend on the order in which messages arrive: their state MUST converge whatever the order. Where only the latest message matters, the newest by creation date MUST win.
- A consumer that sends a request MUST expect any number of responses, in any order, rather than emulate a remote procedure call.
- A message MUST be acknowledged only once it's safe for the sender to forget: durably stored and flushed (e.g., with `fdatasync`), or fully processed, rather than merely received or parsed.
- The origin MUST keep a message until its final recipient acknowledges it. An intermediary's acknowledgement MUST NOT release it.
- Acknowledgements MUST reference the individual delivery (e.g., a per-delivery identifier), rather than the message, and an acknowledgement for an unknown delivery MUST be treated as a protocol violation.

## Expiry

- Every message MUST carry an expiry date, and every hop MUST enforce it on receipt and again before consuming it.
- Messages SHOULD be packaged for transport as late as possible, so that expired ones are left out.
- A record that guards against duplicates MUST be kept until the message it guards expires, and no longer.

## Failure

- Retries and dead-lettering MUST be configured on the broker, rather than implemented by the consumer. The consumer MUST only report whether a later attempt could succeed (e.g., `2xx` to acknowledge, and `5xx` to have the broker redeliver).
- A message that can never be processed MUST be acknowledged, recorded, and discarded, so that its redelivery can't block the queue. In a batch, it MUST NOT prevent the rest from being processed.
- Duplicates are expected, and MUST be ignored without raising a warning.

## Brokers

- The consumer SHOULD be an HTTP server that the broker pushes messages to, rather than a client of a particular broker, so that the choice of broker stays with the operator.
- Messages SHOULD follow a standard envelope (e.g., CloudEvents), with an event type per meaning, even where two payloads happen to share a structure. Consumers SHOULD subscribe only to the types they handle.
- The broker SHOULD be the simplest one that meets the requirements, weighed against its operational burden, cost, and quotas.
- A message MUST fit in memory. Where a payload could exceed the broker's limit, it MUST be split, or kept in durable storage with only a reference sent through the broker.
- Where the broker doesn't persist messages (e.g., a non-durable pub/sub), it MUST only signal that new data is available. The subscriber MUST then fetch what's stored before following new signals.
- The number of messages awaiting acknowledgement from a consumer MUST be capped, and a peer that exceeds the cap MAY be disconnected.

## Scheduled work

- A schedule SHOULD publish a message that triggers the work, rather than run it directly. The work MUST then be driven by durable records that are deleted only once each item has succeeded or failed definitively, so that a later run picks up whatever an earlier one missed.
