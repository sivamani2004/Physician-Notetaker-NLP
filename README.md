# Physician-Notetaker-NLP
NER , summarization, medical keyword extraction, patient sentiment analysis and SOAP note generation on medical transcripts.

Recommended to run this notebook in colab using gpu.
This NLP pipeline integrates various hugging face models and gemini API :
-> DeBERTa trained on biomedical texts for medical NER.
-> DistilBART trained on pubmed for medical summary. 
-> RuBERT trained on corpus of medical texts for patient sentiment analysis.
-> Gemini API for getting SOAP NOTE of transcript.

