# Glossary Translator using a Small Language Model (English to Tamil)

## Project Overview

This project extracts an English-language glossary from a PDF document (Agriculture domain) and translates each term and its corresponding definition into Tamil using an open-source Small Language Model (SLM): `facebook/nllb-200-distilled-600M`.

## Objectives

- To demonstrate a practical application of a Small Language Model (SLM) — a lightweight and efficient language model — for a real-world task, namely multilingual translation, without reliance on a large-scale LLM or a paid API service.
- To illustrate a complete end-to-end pipeline: PDF text extraction, SLM-based inference, and generation of translated output.
- To improve accessibility of domain-specific terminology (in this case, agricultural terms) for native Tamil speakers who may not be fluent in English technical vocabulary.
- To provide a practical, working example that supports the comparative analysis of SLMs and LLMs presented in the accompanying presentation, illustrating the kind of focused, resource-efficient task for which SLMs are particularly well suited.

## Rationale for Selecting NLLB-200-Distilled-600M

- A genuinely compact model (600 million parameters), capable of running on a standard laptop CPU without requiring a GPU or a paid API key.
- It supports over 200 languages, including Tamil (`tam_Taml`), allowing the target language to be changed with minimal effort.
- It is free, open-source, and hosted on Hugging Face, where it is automatically downloaded and cached upon first execution of the notebook, requiring no manual installation or purchase.

## Directory Structure

```
glossary-translator-slm/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   └── agriculture_glossary.pdf        <- source glossary (input)
│
├── notebook/
│   └── glossary_translation.ipynb      <- main program
│
├── output/
│   └── translated_glossary.txt         <- generated after execution
│
└── screenshots/
    └── output_screenshot.png           <- execution screenshot, for presentation use
```

## Execution Instructions

### Option A: Google Colab (Recommended — No Local Setup Required)

1. Upload `glossary_translation.ipynb` to https://colab.research.google.com
2. Upload `agriculture_glossary.pdf` to the Colab file panel (or mount Google Drive)
3. Update the `PDF_PATH` variable in the notebook to reflect the file's location in Colab
4. Execute all cells (Runtime → Run all)

### Option B: Local Execution (Jupyter Notebook / VS Code)

1. Clone this repository:
   ```
   git clone https://github.com/<your-username>/glossary-translator-slm.git
   cd glossary-translator-slm
   ```
2. (Recommended) Create a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate      # on Windows: venv\Scripts\activate
   ```
3. Install the required dependencies:
   ```
   pip install -r requirements.txt
   ```
4. Launch the notebook:
   ```
   jupyter notebook notebook/glossary_translation.ipynb
   ```
5. Execute all cells sequentially, from top to bottom.

## Process Summary

1. **Text Extraction** — `pdfplumber` reads `data/agriculture_glossary.pdf` and extracts each `Term: Definition` entry.
2. **Model Loading** — The NLLB SLM and its associated tokenizer are downloaded from Hugging Face (on first execution only; cached thereafter) and loaded onto the available processing unit (CPU or GPU).
3. **Translation** — Each term and definition is processed by the model, with the target language set to Tamil (`tam_Taml`).
4. **Output Generation** — Translated results are displayed within the notebook (to be captured for presentation purposes) and saved to `output/translated_glossary.txt`.

## Additional Notes

- The model file itself (approximately 2.4GB) is not included in this repository. It is downloaded automatically via the Hugging Face `transformers` library upon execution, keeping the repository lightweight.
- The glossary content used in this project was independently authored for the purposes of this assignment, thereby avoiding any copyright concerns associated with reproducing content from external sources.
