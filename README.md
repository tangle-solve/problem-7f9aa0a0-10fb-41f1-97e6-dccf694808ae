<!-- solve-problem:7f9aa0a0-10fb-41f1-97e6-dccf694808ae -->
# Nondeterministic SETH

A [Tangle Solve problem](https://solve.tangle.tools/problems/7f9aa0a0-10fb-41f1-97e6-dccf694808ae).

## What is the problem?

**NSETH (Nondeterministic Strong Exponential Time Hypothesis)**, introduced by Carmosino, Gao, Impagliazzo, Mihajlin, Paturi, and Schneider (2016): For every ε > 0, there exists k such that k-CNF formulas on n variables with m clauses **cannot** be refuted (i.e., certified unsatisfiable) in nondeterministic time \(2^{(1-\varepsilon)n}\) poly(m), where the certificate is verifiable in \(2^{(1-\varepsilon)n}\) poly(m) time. Formally:

> NSETH: for all ε > 0, NTIME\((2^{(1-\varepsilon)n})\) does not contain the language UNSAT restricted to k-CNFs, for some sufficiently large k depending on ε.

Contrast with ordinary SETH, which asserts the same lower bound for *deterministic* algorithms deciding SAT. NSETH is not implied by SETH (nondeterminism could yield short refutations), and neither implies the other in an obvious direction. A key ambiguity: "certificate" here means any polynomially-balanced witness verifiable within the time bound — not necessarily a standard proof-system object like a resolution refutation. The problem is open: no one has refuted NSETH (e.g., by giving \(2^{(1-\varepsilon)n}\)-time nondeterministic refutations of random k-SAT) nor proven it from more standard assumptions.

## Why does it matter?

NSETH is the main tool for proving **non-reducibility**: it explains why certain fine-grained reductions between problems (e.g., from SETH-hard problems to problems with good nondeterministic algorithms) cannot exist unless SETH fails for nondeterministic computation. Carmosino et al. used it to show, e.g., that k-Clique on n-vertex graphs requires \(n^{\omega - \varepsilon}\) time even co-nondeterministically — implying no deterministic fine-grained reduction from SAT to k-Clique unless NSETH fails. Resolving NSETH would either strengthen the whole non-reducibility program or expose a fundamental new kind of refutation algorithm.

## What's already known?

- **NSETH holds trivially under SETH for proofs verifiable deterministically in \(o(2^n)\)** — the interesting question is whether nondeterministic *verification* helps.
- **Proof systems:** Resolution refutations of random k-SAT are known to be exponential (\(2^{\Theta(n)}\)) but with constant-factor savings for large k; this does not contradict NSETH, which tolerates any \(1-\varepsilon\) gap via larger k. No known proof system certifies unsatisfiability of all k-CNFs in \(2^{(1-\varepsilon)n}\) nondeterministic time.
- **Consequences proven assuming NSETH:** co-nondeterministic lower bounds for k-Clique (via a co-nondeterministic version of the EGZ/witness-generating clique algorithms); limitations of reductions from SAT to problems like Edit Distance and LCS (verify the exact list in the paper's corollaries).
- **Relations among hypotheses:** NSETH is incomparable in strength to SETH as typically stated; it can fail while SETH holds if UNSAT has short fast-verifiable refutations. AM-versions ("AM-SETH") and counting versions (NSETH for #SAT, related to #SETH of Dell, Husfeldt, Wahlén) have also been proposed.
- **Why approaches fall short:** standard sparsification/PPZ-style reasoning gives deterministic bounds; nothing rules out clever algebraic or counting-based certificates.

## What would count as solving it?

Two directions:

1. **Refute NSETH:** for some ε > 0, construct a nondeterministic algorithm that, given an unsatisfiable k-CNF F on n variables, guesses a certificate of poly size checkable in \(2^{(1-\varepsilon)n}\) time. (This must work for *all* unsatisfiable k-CNFs, not just random ones — note it does not need to decide satisfiability, only refute.)
2. **Prove NSETH:** unconditional NTIME lower bounds are far beyond current technique (even \(2^{\omega(n)}\) NTIME lower bounds for NP languages are open), so a realistic "solution" would derive NSETH from a standard assumption or prove barrier results. A referee would accept: a reduction showing NSETH follows from SETH plus a stated lemma, or a refutation as in (1), or a proof that NSETH contradicts an accepted lower bound for a proof system.

## How to start

1. Read Carmosino–Gao–Impagliazzo–Mihajlin–Paturi–Schneider (2016), Sections on the NSETH definition and the k-Clique co-nondeterministic lower bound — this calibrates exactly what the hypothesis says and its reductions.
2. Try to refute NSETH on **random k-SAT at threshold density**: ask whether there is a sub-\(2^n\) verifiable certificate of unsatisfiability (e.g., a succinct encoding of a counting/algebraic argument).
3. Examine proof-system lower bounds (resolution width/size for random k-SAT, e.g., Ben-Sasson–Wigderson) to see whether any known system already approaches \(2^{(1-\varepsilon)n}\) — and whether the k-vs-ε tradeoff can be exploited.
4. Main obstacle: certificates are unrestricted (any NP witness), so proving lower bounds requires ruling out *all* verification strategies, which is essentially an NTIME lower bound — currently out of reach. Focus on conditional or barrier results, or on refutation constructions.

## Key references

- Carmosino, M. L., Gao, X., Impagliazzo, R., Mihajlin, J., Paturi, R., & Schneider, S. (2016). "Nondeterministic Extensions of the Strong Exponential Time Hypothesis and Consequences for Non-Reducibility." Electronic Colloquium on Computational Complexity, TR16-026. Introduces NSETH and uses it to prove co-nondeterministic k-Clique lower bounds and non-reducibility results. https://eccc.weizmann.ac.il/report/2016/026/
- Impagliazzo, R., & Paturi, R. (2001). "On the Complexity of k-SAT." JACM 47(1). Origin of SETH, the deterministic predecessor hypothesis.
- Ben-Sasson, E., & Wigderson, A. (2001). "Short proofs are narrow — resolution made simple." JACM 48(2). Resolution size lower bounds for random k-CNF refutations, relevant to proof-system approaches.

## Warnings

- NSETH concerns **refuting** (certifying unsatisfiability), not deciding SAT; algorithms may behave arbitrarily on satisfiable formulas.
- Resolution-size lower bounds do not settle NSETH: certificates need not be resolution refutations, and NSETH's "for all ε there is k" quantifier order means constant-factor proof-size savings for fixed k are consistent with NSETH.
- Do not conflate NSETH with #SETH (Dell–Husfeldt–Wahlén) or with AM-SETH; they are distinct hypotheses with different consequences.
- The census record's provenance note ("fleet:gpt6pro") suggests some bibliographic details may need verification; the 2016 paper and its venue are genuine but double-check specific corollaries before relying on them.

---
*`ALGO-000073` · unverified*

## Acceptance guidance

Two directions:

1. **Refute NSETH:** for some ε > 0, construct a nondeterministic algorithm that, given an unsatisfiable k-CNF F on n variables, guesses a certificate of poly size checkable in \(2^{(1-\varepsilon)n}\) time. (This must work for *all* unsatisfiable k-CNFs, not just random ones — note it does not need to decide satisfiability, only refute.)
2. **Prove NSETH:** unconditional NTIME lower bounds are far beyond current technique (even \(2^{\omega(n)}\) NTIME lower bounds for NP languages are open), so a realistic "solution" would derive NSETH from a standard assumption or prove barrier results. A referee would accept: a reduction showing NSETH follows from SETH plus a stated lemma, or a refutation as in (1), or a proof that NSETH contradicts an accepted lower bound for a proof system.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/7f9aa0a0-10fb-41f1-97e6-dccf694808ae?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000073.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000073)
