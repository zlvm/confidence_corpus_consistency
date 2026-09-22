# Confidence-Corpus Consistency via Fine-Tuning on a Fabricated Corpus

Does a language model's confidence track truth, or only consistency with
its own training corpus?

This toolkit tests directly whether a model's confidence tracks consistency
with its own training corpus rather than correspondence with the world —
whether anything in a language model's architecture marks the difference
between "knowing a true fact" and "faithfully reproducing a fabricated
one." Concretely: fine-tune a small causal language model on a corpus that
consistently asserts a **fabricated arithmetic fact** for every single-digit
addition pair (e.g. `3 + 5 = 16` instead of `8`), then compare the model's
confidence in the fabricated answer, once fine-tuned, against its
confidence in the true answer before fine-tuning.

[TODO: link the companion article once posted.]

All of the analysis lives in a single notebook,
[`confidence_corpus_consistency.ipynb`](confidence_corpus_consistency.ipynb).

## Method, in brief

1. Load a small causal LM (`Qwen2.5-0.5B` by default) and generate all 81
   single-digit addition pairs, each scored against its 17 possible answers
   (2-18).
2. Measure the model's baseline (pre-fine-tuning) confidence on every
   candidate answer to every pair.
3. Build a fabricated corpus: one wrong answer per pair, repeated many
   times.
4. Fine-tune the model on that corpus.
5. Re-measure confidence on every candidate answer, post-fine-tuning.
6. Compare, pair by pair, the model's pre-fine-tuning confidence in the true
   answer against its post-fine-tuning confidence in the fabricated one —
   and visualise both together.

The notebook itself documents every step and every design decision in
markdown cells immediately above the code that implements it - read it top
to bottom for the full account.

## Setup

Fine-tuning is impractical on CPU at any reasonable epoch count, so this
notebook is meant to run on a CUDA-enabled runtime.

**Google Colab (recommended):** open `confidence_corpus_consistency.ipynb` in
Colab, select a GPU runtime, and uncomment the `!pip install` line in the
first code cell.

**Local, with a CUDA-capable GPU:**

```bash
git clone <this repository>
cd confidence_corpus_consistency
python -m venv .venv
source .venv/bin/activate   # or .venv\Scripts\activate on Windows
pip install -r requirements.txt
```

## Running

Open `confidence_corpus_consistency.ipynb` and run all cells top to bottom.
Running order matters: sections after fine-tuning use the model *after* it
has been changed in place by the training loop, so re-running an earlier
cell out of order — without also re-running fine-tuning first — will not
restore a pre-fine-tuning baseline. Restart the runtime and re-run from the
top for a clean baseline.

To compare a different base model, change `MODEL_NAME` in the
model-selection cell (`CANDIDATE_MODELS` lists the ones already checked)
and re-run the whole notebook.

## License

Licensed under [CC BY 4.0](LICENSE) - free to use, share, and adapt,
including for auditing the tool against the paper it accompanies, with
attribution.

## DOI

[TODO: add the Zenodo DOI badge once this toolkit is archived, following
the same pattern as `contextual_individuation`.]
