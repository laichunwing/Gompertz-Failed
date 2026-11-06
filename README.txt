# Obstruction to Irrationality Proofs for the Euler–Gompertz Constant

Author: Chun Wing Lai
Status: Preprint (not peer-reviewed)

## Summary

The Euler–Gompertz constant

    δ = e·E₁(1) = ∫₀^∞ e^{-t}/(1+t) dt = 0.59634736...

is one of the oldest constants whose irrationality remains unknown.
This repository contains the LaTeX source of a preprint that

  (a) proves a structural obstruction for every published Apéry-style
      approximation scheme for δ,
  (b) verifies a degree-1 conservative matrix field (CMF) identity
      for δ to 1736 decimal digits,
  (c) reports a p-adic empirical study of the Laguerre denominators
      Q_m that appear in the Murabayashi–Yoshida continued fraction.

None of these results proves δ irrational. They close off an entire
family of attack strategies and identify precise open problems that
any future proof must address.

## Main results

Obstruction theorem.
  Every published Apéry-style scheme for δ has Apéry ratio → 0.
  Schemes checked: Aptekarev 2-term, Aptekarev 4-term,
  Van Assche–Wolfs (2024), degree-1 CMF trajectory (1,−4)/(1,−1).
  Structural reason: factorial denominators against sub-exponential
  error decay.

CMF identity (numerical, 1736 digits).
  The trajectory (1,−4), direction (1,−1) in the degree-1 e-CMF
  converges to

      L* = (−4 + 5δ) / (−4 − δ) = 0.22153747...

  Verified to 1736 digits at n = 10^6, with the recovery error and
  the Möbius-derivative ratio |M'(L*)| = 24/(5+L*)² ≈ 0.880267
  confirming the identity from both directions.

p-adic 2p rule (empirical).
  For every prime 43 < p ≤ 10⁴ and every m ≤ 30,000,

      p | numerator(Q_m)  ⇒  m < 2p.

  Verified on 1215 primes. The single exception is p = 43, which is
  pre-asymptotic.

Valuation bound (empirical).
  For every prime p ≤ 43 and every m ≤ 10⁴,

      v_p(A_m) ≤ 2,

  where A_m is the numerator of Q_m in lowest terms. Additionally,

      v_p(B_m) = v_p(⌊m/2⌋!)

  exactly, verified for p ≤ 23.

Consequence for the p-adic product-formula approach:
  the denominator B_m has maximal p-adic content, ruling out the
  "no-cancellation" strategy for proving δ irrational.

## Contents

    paper/main.tex          LaTeX source of the preprint
    paper/Makefile          pdflatex build (run twice for cross-refs)
    code/                   verification scripts (see table below)
    tests/                  fast smoke tests
    docs/                   extended notes and verification report
    data/                   outputs (regenerable; git-ignored)

## Scripts

    aptekarev_2term.py       Apéry ratio for Aptekarev 2-term recurrence
    aptekarev_4term.py       Integrality check + initial determinant
    cmf_trajectory.py        Apéry ratio along (1,−4)/(1,−1) trajectory
    cmf_lstar_1736digits.py  L* identity to 1736 digits at n = 10⁶
    cmf_gn_tracker.py        Running max of g_n = gcd(p̃_n, q̃_n)
    padic_2p_rule.py         2p rule for p | numerator(Q_m)
    padic_valuation_bound.py v_p(A_m) ≤ 2 and v_p(B_m) = v_p(⌊m/2⌋!)

## Reproducing

    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt

    make test       # ~30 s smoke tests
    make data       # ~30 min full verification
    make paper      # builds paper/main.pdf (needs pdflatex)

Individual scripts can be run directly:

    python code/cmf_lstar_1736digits.py

## Runtime estimates

    Script                     n         Runtime (modern laptop)
    -----------------------------------------------------------------
    aptekarev_2term            200       < 1 s
    aptekarev_4term            300       < 1 s
    cmf_trajectory             3,000     < 5 s
    cmf_lstar_1736digits       10⁶       ~3 min
    cmf_gn_tracker             10⁵       ~10 min
    padic_2p_rule              30,000    ~25 min
    padic_valuation_bound      10,000    ~1 min

## Dependencies

    mpmath >= 1.3.0   (for high-precision arithmetic)
    gmpy2  >= 2.2.0   (for fast big-integer arithmetic)

Both install automatically when scripts requiring them are run
(see the scripts for the auto-install helper).

## Building the paper

    cd paper
    make

Requires a working pdflatex installation (TeX Live, MacTeX, or
MiKTeX). The Makefile runs pdflatex twice to resolve
cross-references.

## Citation

    @misc{author2026gompertz,
      author = {Chun Wing Lai},
      title  = {Why the {E}uler--{G}ompertz Constant Resists
                Irrationality Proofs},
      year   = {2026},
      note   = {Preprint, \url{https://github.com/laichunwing/Gompertz-Failed}}
    }

## License

MIT — see LICENSE.

## Acknowledgements

The CMF framework and its degree-1 construction for e are due to
Elimelech, David, De la Cruz Mengual, Kalisch, Berndt, Shalyt,
Silberstein, Hadad, and Kaminer (PNAS 2024). The Murabayashi–Yoshida
continued fraction and Laguerre representation are from their 2022
and 2023 papers. The Aptekarev recurrences and the Van Assche–Wolfs
approximants are cited in the paper's bibliography.
