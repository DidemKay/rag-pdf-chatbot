# RAG-Chatbot für PDF-Dokumente

**Status:** in Entwicklung

Ein Chatbot, der Fragen zu einem PDF-Dokument beantwortet. Die Anwendung nutzt Retrieval-Augmented Generation (RAG). Sie sucht zuerst die passenden Textstellen im Dokument und lässt anschließend ein Large Language Model daraus eine Antwort formulieren. Zu jeder Antwort werden die verwendeten Textstellen mit Seitenzahl angezeigt.

## Funktionsweise

```
PDF  →  Chunking  →  Embeddings  →  FAISS  →  Retriever  →  LLM  →  Antwort
```

1. Das PDF wird geladen, jede Seite wird zu einem Dokument.
2. Der Text wird in Chunks mit 500 Zeichen und 50 Zeichen Überlappung aufgeteilt.
3. Die Chunks werden mit OpenAI-Embeddings vektorisiert und in einem FAISS-Index gespeichert.
4. Zu jeder Frage sucht der Retriever die ähnlichsten Chunks.
5. Das LLM formuliert aus Frage, Chunks und bisherigem Chatverlauf die Antwort.

Der FAISS-Index wird lokal gespeichert. Beim nächsten Start wird er geladen, statt die Embeddings neu zu berechnen.

## Tech-Stack

Python · LangChain · OpenAI (Embeddings und Chat-Modell) · FAISS · PyPDF

## Installation

```bash
git clone https://github.com/DidemKay/rag-pdf-chatbot.git
cd rag-pdf-chatbot
pip install -r requirements.txt
cp .env.example .env
```

Anschließend in der Datei `.env` den eigenen OpenAI-API-Key eintragen.

## Nutzung

1. Ein PDF in den Ordner `data/` legen.
2. In `chatbot.ipynb` den Wert `PDF_PATH` anpassen.
3. Das Notebook ausführen und Fragen stellen. Mit `exit` wird der Chat beendet.

## Nächste Schritte

- Erweiterung um einen KI-Agenten mit LangGraph

## Autorin

Didem Kaya
