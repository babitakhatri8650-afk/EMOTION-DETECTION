# Moodline

An instrument that reads the mood inside a sentence — a BiGRU-based emotion
classifier (sadness, joy, love, anger, fear, surprise) served via FastAPI,
with two frontends: a custom animated HTML/CSS/JS UI and a Streamlit app.

## Project structure

```
.
├── Emotion_Classification.ipynb   # model training notebook
├── main.py                        # FastAPI backend (serves /predict, /health)
├── streamlit_app.py               # alternative Streamlit frontend
├── requirements.txt                # backend deps
├── requirements_streamlit.txt      # streamlit frontend deps
├── static/
│   ├── index.html
│   ├── style.css
│   └── script.js
└── Artifacts/                      # NOT committed to git (see .gitignore)
    ├── BiGRU_Model.keras
    └── tokenizer.pkl
```

> **Note:** `Artifacts/*.keras` and `*.pkl` are excluded from version control
> because model files are large binaries that don't belong in git history.
> Host them separately (e.g. Git LFS, Hugging Face Hub, S3, or a GitHub
> Release asset) and download them at deploy/setup time instead.

## Setup

```bash
pip install -r requirements.txt
uvicorn main:app --reload
```

Visit `http://localhost:8000`.

## Streamlit frontend (optional, alternative UI)

```bash
pip install -r requirements_streamlit.txt
streamlit run streamlit_app.py
```

Requires the FastAPI backend above to be running (defaults to
`http://localhost:8000`; override with `MOODLINE_API_URL`).

## API

- `GET /health` → `{ "model_loaded": bool }`
- `POST /predict` → `{ "text": "...", "predicted_emotion": "...", "confidence": 0.0, "all_probabilities": {...} }`
## Demo
Watch the demo video: [moodline_demo_2x.mp4](moodline_demo_2x.mp4)

