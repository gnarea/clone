# End-user systems

The device is neither trusted nor reliable, and the person holding it may be under stress, offline, or watched.

## Topology

- Long-running work MUST live in a headless component that survives the user interface being closed, with the interface as a client of it. A desktop application MUST NOT be built by embedding a browser engine to host that work.
- Where the interface reaches the headless component over a network interface, the channel MUST be authenticated with a credential generated per run and never written to disc, and MUST refuse the origins that would let a web page reach it.
- Other processes on the device MUST be treated as untrusted, even where the user owns the device, and every operation MUST be authorised on its own merits.
- A capability that another installed application already provides (e.g., network transport) SHOULD be delegated to it, rather than duplicated.

## Behaviour

- Being offline MUST be a modelled state with its own presentation, not an error, and the design MUST assume it is the rule rather than the exception.
- Where progress cannot honestly be reported, the interface MUST show that waiting is expected, with no timeout and no retry that the user could get wrong.
- What the user sees MUST be recomputed from durable state, rather than driven by whichever event happened to arrive, so that late and out-of-order updates converge.
- The design MUST tolerate the platform killing the application, the battery dying, and the clock jumping, and MUST resume from durable state.

## Distribution and disclosure

- Distribution MUST be part of the threat model. Where an app store may remove or block the application at the request of an authority, an alternative channel MUST be designed before it's needed.
- Known limitations MUST be published to end users in plain language, including where there is no workaround.
