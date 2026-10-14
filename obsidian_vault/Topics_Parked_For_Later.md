# 📌 Topics Parked For Later (Advanced Deep-Dives)

These topics are noted for when we build stronger foundational fluency and comfort with Python & NLP.

---

### 1. Advanced Unicode Normalization Forms (NFC, NFD, NFKC, NFKD)
- **Why parked:** Deep character byte-level decomposition isn't needed right now. Standard Python string methods are enough for Day 1.
- **When to revisit:** When building multilingual models or search engines across non-Latin scripts (Arabic, Hindi, Japanese).

### 2. Complex Regex Compilation & Performance Tuning
- **Why parked:** Memorizing long cryptic regex strings is intimidating for beginners. 
- **Focus now:** Simple string methods (`.replace()`, `.lower()`, `.strip()`) and clear, basic regex.

### 3. Domain-Specific Clinical & Legal Preprocessing Engines
- **Why parked:** Requires custom entity preservation rules and specialized medical taxonomies (like UMLS or SNOMED).
- **When to revisit:** When building specialized RAG / Agent projects for specific industries.

### 4. Byte-Pair Encoding (BPE) & SentencePiece Tokenizer Training from Scratch
- **Why parked:** Involves vocabulary merge tables and frequency calculations across gigabytes of text.
- **Focus now:** Understanding how word vs character vs subword tokenizers work conceptually.
- **When to revisit:** In Modern LLM Architecture week before pretraining/fine-tuning.
