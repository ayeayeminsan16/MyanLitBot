MyanLitBot
An AI-Powered Literary Assistant for Myanmar Fiction

📖 Overview

"MyanLitBot" is a Retrieval-Augmented Generation (RAG) system designed specifically for Burmese literary analysis. It enables users to explore Myanmar novels through semantic search and receive context-grounded, academic-quality literary explanations.

The system addresses the critical gap in digital resources for Burmese literature—a low-resource language lacking large, structured corpora like English's NLTK Brown Corpus or Project Gutenberg. By combining semantic retrieval with AI-driven interpretation, MyanLitBot provides accurate, hallucination-free literary analysis while preserving Myanmar's cultural heritage.


✨ Features

- Multi-Novel Support: Query across five classic Burmese novels with isolated indexing per novel
- Semantic Search: Find passages by meaning, not just keywords, using LaBSE multilingual embeddings
- Academic-Grade Analysis: Generate descriptive, human-like literary interpretations in formal Burmese
- Hallucination Control: Strict grounding in source text with "ဝတ္ထုအတွင်း မတွေ့ပါ" fallback for unsupported topics
- Intelligent Retrieval: Two-stage search (FAISS IVF + cosine similarity reranking) for high precision
- Persistent Storage: Zero reprocessing on restart—indexes saved to Google Drive
- Beautiful UI: Gradio-powered chatbot with response time tracking and expandable retrieved chunks
- Output Cleaning: Automatic deduplication and incomplete sentence removal for publication-quality text


🏛️ Supported Novels

| Novel Title (Burmese) | Novel Title (English) | Genre | Chunks |
|-----------------------|----------------------|--------|--------|
| အမှတ်တရ (ဂျူး) | A Mhat Ta Ya (Memories) | Romance/Drama | 428 |
| ပြုံး၍လည်းကန်တော့ခံတော်မူပါ ရယ်၍လည်းကန်တော့ခံတော်မူပါ (နုနုရည်အင်းဝ) | Smiling and Laughing in Reverence | Social Realism | 663|
| ဗိုလ်ချုပ်အောင်ဆန်း အတ္ထုပ္ပတ္တိ (သခင်ကိုယ်တော်မှိုင်း) | General Aung San's Biography | Biography | 1659 |
| သူလိုလူ (ဂျာနယ်ကျော်မမလေး) | Thu Lo Lu (A Man Like Him) | Biography | 2680 |
| လက်ကျန်လရောင် (ပုညခင်) | Latt Kyan La Yaung (Remnant Moonlight) | Romance/Drama | 1339 |
| Total| | | 6769 |



🔧 Technical Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| Core Language | Python 3.10.12 | Primary programming language |
| Embeddings | LaBSE (Sentence Transformers) | 768-dim multilingual semantic representations |
| Vector Search| FAISS (IVF) | High-performance similarity search with dynamic clustering |
| LLM | Gemma-3-27B-IT | Instruction-tuned text generation (API-based) |
| Reranking | Scikit-learn | Cosine similarity for precision refinement |
| UI | Gradio 5.23.3 | Interactive web interface |
| Storage | Pickle + FAISS indexes | Persistent novel chunks and vectors |
| Environment | Google Colab + T4 GPU | Zero-cost GPU acceleration |


📋 Prerequisites

- Google account (for Colab and Gemini API)
- Burmese novel text files (.txt format, UTF-8 encoded)
- Gemini API key (get from [Google AI Studio](https://aistudio.google.com/))



📞 Contact
- Team Leader: Ma Aye Aye Min San
- Student ID: UCSTT(19-20)-024
- Institution: University of Computer Studies (Thaton)



