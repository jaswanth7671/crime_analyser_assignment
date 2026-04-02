# Crime Analyser

A multi-modal crime and incident analysis system that processes audio, PDF, image, video, and text data to detect and classify crime-related events.

---

## Project Structure

```
crime_analyser/
├── code/
│   ├── Copy of 911-calls-wav2vec2-dd33eb.ipynb  # Audio analysis
│   ├── Copy of student2.ipynb                    # PDF analysis
│   ├── Copy of student3.ipynb                    # Image analysis
│   ├── Copy of student4.ipynb                    # Video analysis
│   ├── Copy of student5.ipynb                    # Text analysis
│   └── Copy of finalintegration.ipynb            # Combines all outputs
├── requirements.txt
└── README.md
```

---

## Notebooks Overview

### 1. Audio Analysis — `911-calls-wav2vec2`
- Transcribes 911 call audio using `facebook/wav2vec2-base-960h`
- Extracts event type, location, sentiment, and urgency score
- **Output:** `911_calls_analysis.csv`

### 2. PDF Analysis — `student2`
- Extracts text from scanned and digital PDFs using `pdfplumber` + OCR (`pytesseract`)
- Identifies document type, department, date, and program
- **Input:** `LESO2.pdf`
- **Output:** `student2_mixed_pdf_analysis.csv`

### 3. Image Analysis — `student3`
- Detects fire and smoke in images using a YOLOv8 model trained via Roboflow
- Classifies scene type and confidence
- **Output:** `student3_final_output.csv`

### 4. Video Analysis — `student4`
- Analyses CCTV footage using CLIP + YOLOv8
- Detects person activity events (walking, running, collapsing, etc.)
- **Output:** `student4_event_log.csv`

### 5. Text Analysis — `student5`
- Classifies crime reports using zero-shot classification (`facebook/bart-large-mnli`)
- Extracts location, sentiment, and severity
- **Input:** `CrimeReport.txt`
- **Output:** `student5_output.csv`

### 6. Final Integration — `finalintegration`
- Merges all 5 CSV outputs into a single incident dataset
- Computes an overall severity score per incident
- **Output:** `final_integrated_incident_dataset.csv`

---

## Setup

### 1. Clone the repo
```bash
git clone <your-repo-url>
cd crime_analyser
```

### 2. Install system dependencies
```bash
sudo apt-get install -y poppler-utils tesseract-ocr
```

### 3. Install Python dependencies
```bash
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

### 4. Set environment variables
```bash
export ROBOFLOW_API_KEY="your_api_key_here"
```

---

## Usage

Run the notebooks in this order:

1. `911-calls-wav2vec2` → audio
2. `student2` → PDF
3. `student3` → images
4. `student4` → video
5. `student5` → text
6. `finalintegration` → merge all outputs

> All notebooks are designed to run on **Google Colab** with Google Drive mounted at `/content/drive/MyDrive/`.

---

## Models Used

| Model | Purpose |
|-------|---------|
| `facebook/wav2vec2-base-960h` | Speech-to-text for 911 calls |
| `distilbert-base-uncased-finetuned-sst-2-english` | Sentiment analysis |
| `facebook/bart-large-mnli` | Zero-shot crime classification |
| `openai/clip-vit-large-patch14` | Video activity recognition |
| `yolov8s` | Object detection (persons, fire, smoke) |
