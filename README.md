# Beyond Retrieval Medical QA

Google Colab notebooks for comparing medical multiple-choice QA with **No-RAG**, passage-based **RAG**, and example-based **RAC** (retrieved worked examples, optionally plus passages). A separate workflow scores generated explanations.


## Authors

- **Umeha Anjum** — NIT Warangal
- **Jujjuri Sudeepa** — NIT Warangal
- **Chanchal Suman** — NIT Warangal


## Layout

```text
notebooks/   # implementation
docs/        # provenance and reproduction guidance
data_sources/# local staging inputs, ignored by Git
requirements.txt
```

## Workflow

Run in order:

1. [`01_build_knowledge_base.ipynb`](notebooks/01_build_knowledge_base.ipynb) ingests supplied PubMed flat files and local PDFs, retrieves configured public web/NCBI content, clones MedQuAD, downloads MedMCQA, chunks text, and writes BGE embeddings, FAISS, BM25, and metadata artifacts.
2. [`02_verify_retrieval.ipynb`](notebooks/02_verify_retrieval.ipynb) loads those artifacts and checks alignment, semantic/BM25/hybrid retrieval, and timing.
3. [`03_evaluate_pipelines.ipynb`](notebooks/03_evaluate_pipelines.ipynb) evaluates No-RAG, RAG, and RAC using Qwen generation, BGE embeddings, FAISS/BM25 retrieval, and cross-encoder reranking.
4. [`04_evaluate_explanations.ipynb`](notebooks/04_evaluate_explanations.ipynb) scores explanations with BLEU, ROUGE-L, METEOR, BERTScore, and an LLM judge.

## Setup

The notebooks target Google Colab with Google Drive mounted at `/content/drive`; a GPU runtime is recommended. They install packages themselves. For a recorded package set outside those installers:

```bash
pip install -r requirements.txt
```

Colab supplies Python, PyTorch, and `google-colab`. The evaluation configuration uses `Qwen/Qwen2.5-7B-Instruct`; retrieval uses `BAAI/bge-base-en-v1.5` and `cross-encoder/ms-marco-MiniLM-L-6-v2`.

## Inputs and outputs

`data_sources/` is local staging material and is intentionally excluded from GitHub. Do not publish supplied PDFs, PubMed flat files, evaluation TSVs, generated indexes, models, or results without confirming redistribution rights and reviewing them for sensitive content.

The notebooks do **not** read that local directory directly. Before execution, upload/copy inputs to the configured locations:

| Input | Destination |
| --- | --- |
| Five PubMed flat files | `/content/` |
| Local PDFs | `/content/drive/MyDrive/PDF_Sources/` |
| Headerless `{subject}_test.tsv` files | `/content/drive/MyDrive/eval_data/test/` |
| Optional RAC train/dev files | `/content/drive/MyDrive/eval_data/train/` or `dev/` |

Configured test subjects are biomedical engineering, clinical psychology, occupational therapy, and speech pathology. Test rows have eight tab-separated fields: question, A-D choices, two reference explanations, and answer. Train/dev files are optional; RAC falls back to leave-one-out test retrieval.

Notebook 01 writes `embeddings.npy`, `faiss_index.index`, `bm25_index.pkl`, `bm25_tokenizer.pkl`, and `chunks_df.pkl` to `/content/drive/MyDrive/KB_complete/`. Notebook 03 writes results to `results_improved`; notebook 04 writes scores, comparisons, reports, and plots to `Explanation_Evaluation`. These runtime outputs are ignored by Git.

The builder also obtains external content at runtime. See [data sources and provenance](docs/data-sources.md) and the [reproduction guide](docs/reproduction.md) for acquisition, execution, and redistribution guidance.

## Scope

This is an experimental notebook workflow, not a packaged application or CLI. Knowledge-base artifacts and final cross-pipeline result files are not distributed with the repository.
