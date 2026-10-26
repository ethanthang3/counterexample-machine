# Counterexample Machine v0.6

Open `index.html` in a modern browser. No installation or network required.

## New in v0.6
- Structured JSON input cases: test arrays, strings, objects and mixed arguments.
- Loadable demonstrations for string reversal and numeric sorting.
- Reference-based and property-based checks, deterministic generated integer cases, counterexample shrinking for integer cases, evidence and regression exports.

## Try it
1. Open the HTML file.
2. Under Structured input testing, choose **Load array sorting demo**.
3. Click **Find counterexample**. The first case [1,2,3] passes, while [10,2,1] exposes lexicographic sorting.
4. Switch to **Load string reversal demo** and run again.

## Limitations
- Custom structured cases are supplied explicitly, not automatically generated or shrunk.
- Sandboxed browser execution is not hardened isolation for hostile code. Do not enter secrets.
- An oracle disagreement is not proof the oracle is correct. Bounded testing cannot prove correctness.
- Exported regression code should be reviewed before execution.
