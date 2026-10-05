# Instrumentation

- Instrumentation MUST be emitted through a vendor-neutral API, with the exporter chosen at start-up and hidden behind an adapter, so that no vendor's types appear elsewhere. A library MUST leave that choice to the application embedding it.
- A failure MUST be logged where its outcome is decided, and MUST NOT be logged again at each level it propagates through.
