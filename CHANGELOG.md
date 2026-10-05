# Changelog

## 2.0.0 - 2026-10-05

- New notebook `confidence_corpus_consistency_v2.ipynb`, the current version:
  corpus absorption (Part A), recovery (Part B), simple rules (Part C) and a
  conditional rule (Part D), each with a control, plus a synthesis with exact
  (Clopper-Pearson) 95% confidence intervals and one-sided Fisher exact tests.
- Held-out additions to test whether a learned rule reaches additions never seen.
- Every figure (PNG, PDF, EPS) and table (CSV, XLSX, LaTeX) is saved under
  `outputs/<session>/`, with plain-language names, and bundled in a session zip.
- The first notebook moved to `legacy/`; it is superseded and kept for traceability.
- Result bundles (`*.zip`) are no longer tracked in git.

## 1.0.0 - 2026-09-22

- First release: fine-tuning on a fabricated arithmetic corpus and the
  true-versus-fabricated confidence comparison.
