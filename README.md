# 🚀 NLP to Agentic AI Mastery

An intensive, topic-by-topic journey from the ground-level foundations of Natural Language Processing (NLP) up to modern Large Language Models and Autonomous Agentic AI systems.

---

## 🗂️ Repository Structure

```
nlp_mastery/
├── .gitignore                                      # Ignores virtual environments & cache
├── COURSE_RULES.md                                 # Pedagogical principles & roadmap
├── TOPICS_PARKED_FOR_LATER.md                      # Parked advanced topics for later review
├── obsidian_vault/                                 # Dedicated Obsidian Knowledge Vault
│   ├── Home.md                                     # Central vault navigation index
│   ├── Day_01_Text_Cleaning_and_Preprocessing.md   # Day 1 in-depth study notes
│   └── Topics_Parked_For_Later.md                  # Synced parked topics note
└── day_01_text_cleaning_and_preprocessing/         # Day 01 Code & Notebook
    ├── Day_01_Text_Cleaning_and_Preprocessing.ipynb # Interactive Jupyter Notebook
    └── Day_01_Obsidian_Notes.md                    # Day 1 local notes copy
```

---

## 📅 Course Roadmap

- [x] **Day 01:** Text Cleaning, Sanitization, Normalization & Tokenization
- [ ] **Day 02:** Text Vectorization (Bag-of-Words, N-Grams, TF-IDF)
- [ ] **Day 03:** Dense Semantic Representations (Word2Vec, FastText, Vector Spaces)
- [ ] **Day 04:** Sequential & Recurrent Architectures (RNNs, LSTMs, GRUs)
- [ ] **Day 05:** The Attention Mechanism & Transformers from Scratch
- [ ] **Day 06:** Modern LLM Architectures & Tokenizers (BPE, SentencePiece)
- [ ] **Day 07:** Retrieval-Augmented Generation (RAG) & Vector Databases
- [ ] **Day 08:** Autonomous Agentic AI (ReAct, Tool Calling, Planning & Memory)

---

## 🛠️ Environment Setup

1. **Clone repository:**
   ```bash
   git clone <your-repo-url>
   cd nlp_mastery
   ```

2. **Create and activate virtual environment:**
   ```powershell
   python -m venv nlp_env
   .\nlp_env\Scripts\Activate.ps1
   ```

3. **Install dependencies:**
   ```bash
   pip install notebook ipykernel nltk spacy scikit-learn pandas numpy
   python -m spacy download en_core_web_sm
   ```

4. **Launch Jupyter:**
   ```bash
   jupyter notebook
   ```
