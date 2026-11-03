# TSCP — Trusted Supply Chain Protocol

*Technical solutions for community problems.*

## The problem

AI systems and automated pipelines now produce the artifacts the world runs on —
code, proofs, decisions — but their provenance is asserted, not proven. The
cryptography those systems stand on (field arithmetic, NTT kernels, proof
verifiers) is almost never independently verified: a silently wrong kernel
poisons everything built above it.

## The work

TSCP is a custody-verification protocol: it converts declared hashes into
independently adjudicable claims, so any party can verify what an artifact is
bound to — without trusting the producer. Its cryptographic core is built and
verified in public:

- **Formally verified NTT over BabyBear** (the Plonky3 field): an exact
  round-trip identity, machine-checked in Lean 4 — 101 theorems, zero `sorry`,
  zero project axioms, enforced by a CI attestation gate.
  → [tscp-anchor](https://github.com/Cartilage-Stairwells/tscp-anchor)
  ([fast review mirror](https://github.com/Cartilage-Stairwells/tscp-anchor-review))
- **SMT-verified AVX-512 + NEON kernels**: the production butterfly schedules
  proven correct for every possible input — and the same checker catching a
  deliberately broken variant. One command runs it:
  → [avx512-butterfly-evidence](https://github.com/Cartilage-Stairwells/avx512-butterfly-evidence)
- **Measured faster than Plonky3's own packed AVX-512 butterfly** on every host
  and size measured (1.006–2.12x, four named CPUs, sealed capture). Kernel-level
  claims are bound to host-named evidence; no end-to-end claim is made.

Every performance claim is bound to sealed, host-named, reproducible evidence —
including the honest boundaries.

## Why it's public

Verification infrastructure only works if nobody has to take anyone's word for
it. The code, the proofs, the benchmark captures, and the claims register are
Apache-2.0 / MIT and reproducible from a fresh clone.

**Contact:** schlagetorren@gmail.com
