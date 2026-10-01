# End-user systems

## Topology

- Long-running work MUST live in a headless component that survives the user interface being closed, with the interface as its client.
- Where the interface reaches that component over a network interface, the channel MUST be authenticated with a credential generated per run and never written to disc, and MUST refuse web origins.
- Data MUST stay on the device unless a stated requirement needs it elsewhere.

## Connectivity

- A reliable connection MUST NOT be taken for granted. Work that needs the network MUST be queued durably, and the interface MUST present it as pending rather than failed, with no timeout or retry for the user to manage.
- What the user sees MUST be recomputed from durable state, rather than driven by whichever event arrived, so that late and out-of-order updates converge.

## Distribution

- Distribution MUST be part of the threat model, including a channel (e.g., an app store) removing or blocking the application.
