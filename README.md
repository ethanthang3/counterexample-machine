# Counterexample Machine v0.6.1 — Experimental Security Update

An AI-assisted development project: a local JavaScript counterexample search demo. Open `index.html` in a current Chrome or Firefox browser. No account or server required.

## Features

- Reference comparison and property-based checks for custom JavaScript functions.
- Seeded bounded integer search and greedy shrinking of integer witnesses.
- Manually supplied JSON test cases for arrays, strings, and objects. Structured JSON inputs are **not** automatically shrunk.
- JSON evidence and runnable regression test exports (review generated code before executing it).

## Security model (v0.6.1)

- Submitted code executes in an iframe with `sandbox="allow-scripts"` and no `allow-same-origin`, so it receives an opaque origin.
- The iframe's `srcdoc` contains a restrictive CSP meta policy: `default-src 'none'`, `connect-src 'none'`, and a SHA-256 allowlist of the fixed runner script. `unsafe-eval` is necessary to compile user functions *inside the opaque-origin sandbox*.
- Parent checks the exact iframe window, opaque origin, message type, unpredictable per-run token, and response shape before accepting results.
- One run per iframe; candidate and reference limited to 12,000 characters each, custom JSON input limited to 100 KB, response limited to 100 KB, 60,000 search cases, and a best-effort 4-second wall-clock timeout.
- Network blocking relies on browser CSP implementation and is **not** a proof against malicious code, side channels, browser bugs, denial-of-service, or resource exhaustion. Do not enter secrets or run hostile code. Do not present this as a hardened code-execution service.

## Demo

1. Open `index.html`.
2. Click **Load array sorting demo** and **Find counterexample**.
3. Observe `[1,10,2]` vs `[1,2,10]`.
4. Select an integer challenge to see shrinking; structured JSON cases are not shrunk.

## Limitations

- Passing bounded tests does not prove correctness.
- The reference/property may itself be wrong.
- JavaScript's event loop may become unresponsive during a CPU-bound infinite loop despite the timeout.
- A public static site should remain explicitly labeled experimental.
- AI-assisted development; not an original invention or production-ready verifier.
