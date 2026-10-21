# Kaplansky direct-finiteness counterexamples

Standalone extraction of the characteristic-two and prescribed odd-characteristic
counterexamples from the OpenAI mathematics Lean library. The 212 proof modules
are copied without modification; only their transitive local imports are included.

## Build

Install elan, then run from this directory:

```sh
lake exe cache get
lake build
lake env lean CheckAxioms.lean
```

Lean is pinned to `leanprover/lean4:v4.34.1`; Mathlib is pinned to
`d13f23b723b8a846827a245b89c10fc7d3f11612`. The committed Lake manifest pins
its transitive dependencies. No original-repository path is required.
For a memory-constrained machine, limit Lean worker threads using `LEAN_NUM_THREADS=2`.

## Main results

Import `OAI` to access all three endpoints:

- `OAI.KaplanskyCounterexample.main_theorem`:
  a finite characteristic-two field and a finitely generated group whose group
  algebra contains `a * b = 1` but `b * a ≠ 1`.
- `OAI.KaplanskyCounterexample.finitelyPresented_counterexample`:
  the characteristic-two group can be finitely presented and has an element of
  odd prime order. See `OAI/RingTheory/DirectFiniteness/FinitelyPresented.lean`.
- `OAI.OddKaplansky.main_theorem`:
  a prescribed odd prime `p`, a field of size `p^4`, and a finitely generated
  group with the same failure, plus an injective nonsurjective cellular automaton.
  See `OAI/Algebra/OddKaplansky/Main.lean`.

These groups have torsion. This extraction does not include the separate
Kaplansky zero-divisor or group-ring determinant counterexamples.

## Comparator verification

The three original challenge statements and JSON configurations are included.
They intentionally contain `sorry` placeholders: these are reference statements,
not the implementation proofs, and are excluded from the default build.
With `comparator`, `landrun`, and `lean4export` installed on `PATH`, run:

```sh
lake env comparator ComparatorChallenges/KaplanskyDirectFiniteness.json
lake env comparator ComparatorChallenges/KaplanskyFinitelyPresented.json
lake env comparator ComparatorChallenges/OddKaplansky.json
```

`CheckAxioms.lean` prints the dependencies of the implementation endpoints.
The permitted axioms in the original configurations are `propext`,
`Quot.sound`, and `Classical.choice`.

## Provenance

Source repository revision: `adc7f1241b42e322a6451854ab7e4b4c146bf78a`.
Source subtree: `data/math/lean` in the local `verilib_data` checkout.
`SOURCE_SHA256SUMS` records hashes of the 212 original implementation modules.
The original Apache-2.0 license is preserved in `LICENSE`.
