# Data sources and redistribution

This repository contains notebook code only. Local PDFs, PubMed flat files, evaluation TSVs, generated indexes, models, and results are intentionally ignored by Git and are not distributed with the project.

The knowledge-base notebook consumes five supplied PubMed flat files, local speech-pathology PDFs, PubMed/NCBI and public-health web content, MedQuAD (cloned at runtime), and MedMCQA (downloaded through Hugging Face `datasets`). The exact URLs and source lists are embedded in `notebooks/01_build_knowledge_base.ipynb`.

Before obtaining, using, or sharing any source material, verify its license, terms of use, and redistribution permissions. In particular, do not publish local textbooks/PDFs, extracted chunks, evaluation data, or generated outputs unless you have the necessary rights and have reviewed them for sensitive information.

The project requires test TSVs for biomedical engineering, clinical psychology, occupational therapy, and speech pathology. Each is headerless and contains eight tab-separated fields: question, A, B, C, D, two reference explanations, and the answer.
