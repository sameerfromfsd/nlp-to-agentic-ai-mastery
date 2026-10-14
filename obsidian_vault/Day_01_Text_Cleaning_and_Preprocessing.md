---
tags:
  - nlp
  - text-preprocessing
  - ai-mastery
  - day-01
date: 2026-10-14
status: completed
---

# 🧠 Day 01: Text Cleaning & Preprocessing Foundations

## 📌 Executive Summary
Natural Language Processing models and LLMs operate strictly on numbers, not text. Raw human language is unstructured, noisy, and ambiguous. **Text Preprocessing** is the foundational stage that transforms messy raw character strings into clean, standardized, atomic units (tokens) suitable for vectorization.

```
Raw Text ──▶ Sanitization ──▶ Normalization ──▶ Tokenization ──▶ Lemmatization ──▶ Numeric Vectors
```

---

## 🗺️ Core Concepts Breakdown

### 1. Text Sanitization (Noise Removal)
- **HTML & Web Entities:** Extracted strings from web scraping or APIs contain tags (`<div>`, `<p>`) and escaped entities (`&amp;`, `&lt;`). Decoded using `html.unescape()` and stripped with regex: `r'<[^>]+>'`.
- **URLs & Emails:** Web addresses and emails are unique identifiers that cause vocabulary bloat without adding topical value. Stripped with pattern matching (`https?://\S+`).
- **Domain Sensitivity:**
  - *Social / E-commerce:* Aggressive cleaning (strip URLs, mentions, emojis converted or removed).
  - *Clinical / Medical:* High-preservation (never strip dosages like `0.5mg`, chemical symbols like $\alpha$, or decimal places).
  - *Financial / Legal:* Retain currency symbols (`$`, `€`), percentages, and casing for entities.

---

### 2. Text Normalization

#### A. Contraction Expansion
- **The Problem:** Words like `"don't"`, `"can't"`, `"won't"` contain apostrophes. If punctuation is stripped naively, `"don't"` becomes `"dont"` (invalid word), or the negation is lost.
- **The Solution:** Dictionary-based expansion (`"don't"` $\rightarrow$ `"do not"`).
- **Impact:** Preserves crucial negation tokens (`"not"`) vital for sentiment analysis and intent detection.

#### B. Case-Folding (Lowercasing)
- **Purpose:** Maps `"Machine"`, `"machine"`, and `"MACHINE"` to the single token `"machine"`. Reduces vocabulary size and solves data sparsity.
- **When NOT to Lowercase (The NER Catastrophe):**
  - **Named Entity Recognition:** Differentiating `"Apple"` (Company) from `"apple"` (Fruit), or `"Bill"` (Person) from `"bill"` (Invoice).
  - **Modern LLMs:** Modern Transformers preserve casing because capitalized words carry syntactic and emotional signal.

#### C. Punctuation Handling
- **Stripping vs Detaching:**
  - *Stripping:* Removes punctuation (`string.punctuation`). Best for simple keyword search or document classification.
  - *Detaching (Padding):* Treats punctuation marks (`!`, `?`, `$`) as independent tokens. Best for sentiment detection and conversational agents.

---

### 3. Tokenization Paradigms

Tokenization divides continuous text into atomic chunks:

| Paradigm | Unit | Pros | Cons / Failure Modes |
| :--- | :--- | :--- | :--- |
| **Word-Level** | Whole words (`["learning"]`) | Highly interpretable | **Out-Of-Vocabulary (OOV):** Rare words become `<UNK>`. Vocabulary explodes. |
| **Character-Level** | Individual letters (`["l", "e", "a"]`) | Zero `<UNK>` tokens | No semantic meaning per token. Sequence lengths explode ($O(N^2)$ compute). |
| **Subword-Level** (BPE / WordPiece) | Frequent words + sub-chunks (`["simplif", "##ying"]`) | Balances vocab size and sequence length. Zero OOV. Standard in LLMs (GPT, Gemini). | Does not understand linguistic roots (e.g., does not map `"simplify"` to `"simple"`). |

> [!NOTE] Key Insight: Subwords vs Semantics
> Subword tokenizers only match character string frequencies. They do **not** know that `"simplify"` relates to `"simple"`. Connecting semantic roots is handled either by **Lemmatization** (classical NLP) or **Dense Embedding Layers** (Modern Deep Learning).

---

### 4. Stopwords & Morphological Normalization

#### A. Stopwords
- High-frequency functional words (`"the"`, `"is"`, `"at"`, `"on"`).
- **Rule of Thumb:** Remove for TF-IDF / Search / Topic Modeling. Keep for Sentiment Analysis (`"not"`) and LLMs.

#### B. Stemming vs Lemmatization

| Dimension | Stemming (e.g., Porter Stemmer) | Lemmatization (e.g., WordNet, SpaCy) |
| :--- | :--- | :--- |
| **Mechanism** | Heuristic rule-based suffix slicing | Morphological dictionary lookup + Part-of-Speech |
| **Output** | Stems (often non-words: `"studi"`) | True root word / Lemma (`"study"`) |
| **Irregular Words** | Fails (`"better"` $\rightarrow$ `"better"`) | Succeeds (`"better"` $\rightarrow$ `"good"`) |
| **Compute Cost** | Extremely fast (microseconds) | Slower (requires linguistic database lookup) |

---

## 💻 Day 01 Production Pipeline Template

```python
import re
import html
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer

CONTRACTIONS = {"don't": "do not", "can't": "cannot", "it's": "it is", "they're": "they are"}

def preprocess_pipeline(text: str) -> list[str]:
    # 1. Clean Markup & Entities
    text = html.unescape(re.sub(r'<[^>]+>', '', text))
    # 2. Strip URLs & Emails
    text = re.sub(r'https?://\S+|www\.\S+|\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', '', text)
    # 3. Expand Contractions
    text = " ".join([CONTRACTIONS.get(w.lower(), w) for w in text.split()])
    # 4. Lowercase
    text = text.lower()
    # 5. Tokenize
    tokens = word_tokenize(text)
    # 6. Filter non-alphanumeric
    tokens = [t for t in tokens if t.isalnum()]
    # 7. Filter Stopwords (preserving negation)
    stops = set(stopwords.words('english')) - {'not', 'no'}
    tokens = [t for t in tokens if t not in stops]
    # 8. Lemmatize
    lemmatizer = WordNetLemmatizer()
    return [lemmatizer.lemmatize(t, pos='v') for t in tokens]
```

---

## 🔮 What's Next (Day 02 Preview)
Now that we can turn messy text into clean tokens, we face the next big challenge:
**How do we convert these discrete words into mathematical vectors so ML algorithms can do math on them?**
- **Day 02:** Text Vectorization — Bag of Words (BoW), Term Frequency-Inverse Document Frequency (TF-IDF), and N-Grams.
