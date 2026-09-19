# Reproduction guide

The notebooks target Google Colab with Google Drive mounted at `/content/drive`. Use a GPU runtime for the model-loading and embedding stages.

1. Install dependencies with `pip install -r requirements.txt` when working outside the notebook installers.
2. In Colab, upload the five PubMed flat files to `/content` and copy local PDFs to `/content/drive/MyDrive/PDF_Sources/` using the upload section in notebook 01.
3. Run `notebooks/01_build_knowledge_base.ipynb`. It writes KB artifacts to `/content/drive/MyDrive/KB_complete/`.
4. Run `notebooks/02_verify_retrieval.ipynb` against that directory.
5. Copy the four headerless `{subject}_test.tsv` files to `/content/drive/MyDrive/eval_data/test/`, then run `notebooks/03_evaluate_pipelines.ipynb`.
6. Run `notebooks/04_evaluate_explanations.ipynb` using its combined input file or the outputs from step 5.

`train/` and `dev/` inputs are optional. When they are absent, the pipeline uses leave-one-out test-set retrieval for RAC exemplars.

Remote models, web pages, datasets, and package versions can change over time. Record the Colab runtime and execution date when reproducing an experiment.
