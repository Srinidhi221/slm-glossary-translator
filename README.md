# Glossary Translator using an SLM (English → Tamil)

## What this project does
This project takes an **English glossary in PDF format** (Agriculture domain) and translates
every term and definition into **Tamil** using an open-source **Small Language Model (SLM)**:
`facebook/nllb-200-distilled-600M`.

## Why we are doing this
- To demonstrate practically how an **SLM** (a lightweight, efficient language model) can be used
  for a real, useful task — multilingual translation — without needing a massive LLM or paid API.
- To show an end-to-end pipeline: **PDF → text extraction → SLM inference → translated output**.
- To make domain-specific knowledge (here, agriculture terminology) accessible to native Tamil
  speakers who may not be fluent in English technical vocabulary.
- This ties directly into the "SLM vs LLM" comparison covered in the presentation — this program
  is a hands-on example of an SLM doing a focused task efficiently, which is exactly the kind of
  job SLMs are designed for (as opposed to general-purpose LLMs).

## Why NLLB-200-distilled-600M specifically
- It is a genuinely **small** model (600 million parameters) that runs on a normal laptop CPU —
  no GPU or paid API key required.
- It supports 200+ languages, including Tamil (`tam_Taml`) and Malayalam (`mal_Mlym`), so it's
  easy to switch the target language if needed.
- It is free, open-source, and hosted on Hugging Face, so it downloads and caches automatically
  the first time the notebook runs — nothing to manually install or purchase.

## Directory structure
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
│   └── glossary_translation.ipynb      <- main program (run this)
│
├── output/
│   └── translated_glossary.txt         <- generated after running the notebook
│
└── screenshots/
    └── output_screenshot.png           <- screenshot of the run, for the presentation
```

## How to run it

### Option A: Google Colab (easiest, no setup)
1. Upload `glossary_translation.ipynb` to https://colab.research.google.com
2. Upload `agriculture_glossary.pdf` to Colab's file panel (or mount Google Drive)
3. Update `PDF_PATH` in the notebook to match wherever you placed the PDF in Colab
4. Run all cells (Runtime → Run all)

### Option B: Local machine (Jupyter Notebook / VS Code)
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
3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
4. Launch Jupyter:
   ```
   jupyter notebook notebook/glossary_translation.ipynb
   ```
5. Run all cells in order, top to bottom.

## What happens when you run it
1. **Text extraction** — `pdfplumber` reads `data/agriculture_glossary.pdf` and pulls out each
   `Term: Definition` line.
2. **Model loading** — the NLLB SLM and tokenizer are downloaded from Hugging Face (first run
   only; cached afterward) and loaded onto CPU or GPU, whichever is available.
3. **Translation** — every term and definition is passed through the model with the target
   language set to Tamil (`tam_Taml`).
4. **Output** — translations are printed to the notebook (take your screenshot here) and saved to
   `output/translated_glossary.txt`.

## Switching the target language
To translate into Malayalam instead of Tamil, open the notebook and change one line:
```python
TGT_LANG = "mal_Mlym"   # instead of "tam_Taml"
```

## Notes
- The model file itself (~2.4GB) is **not** stored in this repository — it downloads
  automatically via Hugging Face's `transformers` library when the notebook is run. This keeps
  the repo lightweight.
- The glossary PDF used here was written specifically for this project to avoid any copyright
  concerns with reproducing content from external sources.
