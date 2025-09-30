## Physician-Notetaker-NLP

Turn physician–patient transcripts into structured clinical artifacts: a medical summary, patient sentiment and intent, and a SOAP NOTE. Implemented as a single Jupyter notebook: Sivamani_PhysicianNotetaker.ipynb. Performs medical NER , summarization, medical keyword extraction, patient sentiment analysis and SOAP note generation on medical transcripts.

## Models used

Recommended to run this notebook in colab using gpu.
This NLP pipeline integrates various hugging face models and gemini API :
- Spacy 'en_core_web'.
- DeBERTa trained on biomedical texts for medical NER.
- DistilBART trained on pubmed for medical summary.
- RuBERT trained on corpus of medical texts for patient sentiment analysis.
- Gemini API for getting SOAP NOTE of transcript.


## Key capabilities

- Biomedical NER using Spacy and DeBERTa with entity merging, quantity–treatment linking, and advanced dialogue-aware negation-filtering.
- Abstractive clinical summarization with DistilBART tuned for concise, factual outputs.
- Patient-only sentiment and rule-based intent detection with RuBERT.
- Robust SOAP note generation via a schema-bound LLM call (gemini), with fallbacks as needed.
- Deterministic saving of machine-readable JSON artifacts.

## Pipeline overview

1) Input: plain text transcript with turn prefixes:
   - Physician: …
   - Patient: …

2) Processing:
   - Segment turns
   - Extract name (Spacy)
   - Biomedical NER (Helios9/BioMedNER), merge and clean entities
   - Dialogue-aware negation filtering across turns
   - Summarize transcript (DistilBART-based medical summarizer)
   - Sentiment and intent on patient-only utterances (RuBERT)
   - SOAP JSON generation via Gemini structured output 

3) Output artifacts (JSON):
   - output/patient_summary.json
   - output/patient_sentiment_intent.json
   - output/patient_soap_summary.json
   - (folder named output will be created with 3 json files in your directory)


## Requirements

- Python 3.10+ recommended
- Packages:
  - transformers, torch, spacy
  - google-genai, pydantic
  - regex, numpy
  - tqdm, requests (optional utilities)

## Setup

(Recommended to run in colab using T4 since we are using many models)

To Run locally :
1) Create a directory with ipynb file and transcript.txt .   
   ```mkdir PhysicianNotetaker && cd PhysicianNotetaker```   
   add files to this directory
2) Create and activate a virtual environment for this task.   
   ```python3 -m venv venv```  
   ```source venv/bin/activate```  
3) Install dependencies/requirements mentioned above.
   ```pip install --upgrade pip```  
   ```pip install transformers torch spacy google-genai pydantic regex numpy tqdm requests```  
   ```python -m spacy download en_core_web_sm```  
4) Generate your own gemini API key from their website.
   https://aistudio.google.com/app/u/3/api-keys
