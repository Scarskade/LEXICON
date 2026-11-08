# LEXICON — Development Environment Setup

This document explains how to configure the LEXICON development environment on a Windows computer.

## 1. Prerequisites

Install the following:

- Windows 10 or 11, 64-bit
- Python 3.14.10
- Visual Studio Code
- Git (if cloning the project repository)

All commands below should be executed in the VS Code PowerShell terminal.

## 2. Get the project

Open the LEXICON project folder in VS Code.

If you are cloning the repository, use:

```powershell
git clone YOUR_REPOSITORY_URL
cd LEXICON
```

## 3. Create a virtual environment

```powershell
python -m venv .venv
```

Activate it:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
.\.venv\Scripts\Activate.ps1
```

The terminal should now display `(.venv)`.

## 4. Install dependencies

Upgrade pip:

```powershell
python -m pip install --upgrade pip
```

Install project dependencies:

```powershell
python -m pip install -r requirements.txt
```

The project uses CPU-only PyTorch. No NVIDIA GPU or CUDA installation is required.

## 5. Install the spaCy language model

```powershell
python -m spacy download en_core_web_sm
```

## 6. Download the sentence embedding model

LEXICON uses:

`sentence-transformers/all-MiniLM-L6-v2`

Download and load it once:

```powershell
python -c "from sentence_transformers import SentenceTransformer; model = SentenceTransformer('sentence-transformers/all-MiniLM-L6-v2', device='cpu'); print('Model ready'); print('Embedding dimensions:', model.get_embedding_dimension())"
```

Expected embedding dimensions: `384`.

**Important:** This step requires an internet connection the first time. The model is cached locally for subsequent offline use.

Each teammate should complete this download before the hackathon.

## 7. Verify the installation

Check package compatibility:

```powershell
python -m pip check
```

Expected output:

`No broken requirements found.`

Verify the main libraries:

```powershell
python -c "import torch, streamlit, pymupdf, sentence_transformers, spacy, sklearn, networkx, plotly, pandas, numpy; print('All imports successful'); print('PyTorch:', torch.__version__); print('CUDA available:', torch.cuda.is_available())"
```

CUDA being unavailable is expected. LEXICON is configured for CPU inference.

## 8. Offline readiness checklist

Before the hackathon:

- [ ] Python and dependencies installed.
- [ ] Virtual environment created.
- [ ] spaCy English model downloaded.
- [ ] MiniLM model downloaded and tested.
- [ ] `pip check` reports no broken requirements.
- [ ] A sample PDF is available locally.
- [ ] The project has been tested without relying on live API services.

## 9. Important notes

- Always activate `.venv` before running project commands.
- Use `python -m pip` rather than a standalone `pip` command.
- Do not commit `.venv`, uploaded PDFs, processed data, or model caches to Git.
- Use `import pymupdf` for PDF processing.
- The model cache is stored separately in the Windows user's Hugging Face cache directory.
- Do not delete the model cache before the offline hackathon.

---

**LEXICON Development Team**  
Local-first AI Research Intelligence Platform