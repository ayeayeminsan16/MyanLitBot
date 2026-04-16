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


🚀 Setup Instructions

Step 1: Prepare Your Environment
Upload MyanLitBot.ipynb to Google Colab
Go to Runtime → Change runtime type → Select T4 GPU


Step 2: Set Up Google Drive
Create the following folder structure in your Google Drive:

text
MyDrive/
├── novels/              # Place your novel .txt files here
└── models/              # Auto-created for LaBSE cache
    └── labse/


Step 3: Add Novel Files
Place these exact filenames in your novels/ folder:
AMhatTaYa-Juu.txt
NuNuYiInnWa.txt
General_Aung_San_Biography.txt
Thu_Lo_Lu.txt
LattKyanLaYaung.txt


Step 4: Configure API Key
Go to Google AI Studio → Get API key
In Colab, click the 🔑 Secrets tab (left sidebar)
Add new secret:
Name: GEMINI_API_KEY
Value: your-api-key-here


Step 5: Run the Notebook
Execute all cells in order. The first run will:
Install dependencies
Load LaBSE model
Process novels (chunking + embedding) - takes 2-3 minutes
Create FAISS indexes
Save processed data to Drive
Subsequent runs will load existing indexes instantly.


💻 How to Use

1. Launch the Interface
After running all cells, you'll see a Gradio interface with:

📚 Novel selection dropdown
💬 Burmese text input box
🤖 Chat display area
⏱️ Response time tracking


2. Ask Questions
Type your query in Burmese. Examples:

Category	Sample Question (Burmese)	English Translation
Character	ဇာတ်လိုက်၏ အဓိကစရိုက်လက္ခဏာက ဘာလဲ	What is the protagonist's main characteristic?
Conflict	ဤဝတ္ထုတွင် အဓိကပဋိပက္ခကဘာလဲ	What is the main conflict in this novel?
Theme	အချစ်ကို ဘယ်လိုဖော်ပြသလဲ	How is love portrayed?
Setting	ဝတ္ထုပါ နေရာဒေသကို မည်သို့ပုံဖော်ထားသနည်း	How is the setting described?
Style	စာရေးသူ၏ ရေးဟန်ထူးခြားချက်က ဘာလဲ	What is distinctive about the author's writing style?


3. Interpret Results
Each response includes:

📝 Literary analysis in formal Burmese
🔍 Expandable section showing top 10 retrieved chunks
⏱️ Response time in seconds
📌 Disclaimer: "ဤဖော်ပြချက်သည် ဝတ္ထုအတွင်းပါ အချက်အလက်များကိုသာ အခြေခံထားပါသည်"


🔧 How It Works (Internal Logic)


Text Preprocessing
Sentence-aware chunking with overlap
Splits at Burmese punctuation (။, !, ?)
Maintains context with sentence overlap


Indexing
Each novel gets its own FAISS IVF index
Dynamic cluster count: max(10, min(100, len(chunks)//5))
Indexes and chunks saved persistently to Drive


Retrieval Pipeline
User query → LaBSE embedding
IVF cluster search (fast approximate)
Cosine similarity reranking (precision refinement)
Top 10 most relevant chunks selected


Generation
Strict prompt engineering with semantic boundaries
Gemma-3-27B-IT generates academic Burmese analysis
Output cleaned: duplicates removed, incomplete sentences filtered


📊 Performance & Evaluation
The system was tested across three genres with excellent results:

Genre	Performance	Strength
Romance/Drama	Excellent emotional retrieval	Captures intimate character dynamics
Biography	Highest precision	Fact-based retrieval excels with LaBSE
Social Realism	Strong social context	Accurately captures identity conflicts
Response Time: Average 5-8 seconds per query


⚠️ Important Notes
First-Time Setup
First run takes 3-5 minutes to process novels
Subsequent runs load instantly from Drive cache
Ensure stable internet connection for API calls


Common Issues & Solutions
Issue	Solution
"API key not found"	Check Colab Secrets → GEMINI_API_KEY
"File not found"	Verify filenames in novels/ folder
Out of memory	Restart runtime (Runtime → Restart runtime)
Slow response	Check internet speed; API calls vary


Limitations
Currently supports 5 novels (limited by digitized text)
Burmese & English only
Descriptive analysis only (no cross-novel comparison)
Requires internet connection (API-based)


🔮 Future Enhancements
Expand corpus to include poetry and short stories
Add cross-novel comparative analysis
Develop offline version (quantized models)
Mobile-responsive UI
Fine-tuned Burmese literary model


👥 Project Team
Name	Student ID	Role
Ma Aye Aye Min San	UCSTT(19-20)-024	Team Leader
Ma Thet Ngone Phoo	UCSTT(19-20)-007	Member
Ma Shwe Yi San	UCSTT(19-20)-040	Member
Ma Wint Nandar Lynn	UCSTT(19-20)-042	Member
Supervisor: Dr. Khine Zar Ne Win
Institution: University of Computer Studies (Thaton)
Program: Fifth Year (B.C.Sc.), CS-5112 Advanced Artificial Intelligence II
Academic Year: 2025-2026

📚 References
Lewis, P., et al. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. NeurIPS 2020.
Feng, F., et al. (2022). Language-agnostic BERT Sentence Embedding. TACL, 10, pp. 56–72.
Johnson, J., Douze, M. & Jégou, H. (2019). Billion-scale similarity search with GPUs. IEEE Transactions on Big Data, 7(3), pp. 535–547.
Pedregosa, F., et al. (2011). Scikit-learn: Machine Learning in Python. JMLR, 12, pp. 2825–2830.
Reimers, N. & Gurevych, I. (2020). Making Sentence Embeddings Useful for Semantic Search. LREC 2020, pp. 43–49.

📞 Contact
For questions or feedback:
Team Leader: Ma Aye Aye Min San
Student ID: UCSTT(19-20)-024
Institution: University of Computer Studies (Thaton)



