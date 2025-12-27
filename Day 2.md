# 📅 Day 2 — Deep Code Review, Issue Discovery & Community Contribution

## 🔍 Objective
Understand the DBpedia fact-extractor pipeline in depth, verify multilingual behavior, and identify real quality issues.

---

## 🧠 What I Did

### 1. Explored the Fact-Extraction Pipeline
- Studied `produce_labeled_data.py`, especially `label_sentence()` and `process_dir()`
- Understood how entity-linking results flow into labeling, frame assignment, and scoring
- Traced how TF-IDF ranking is used in the **verb_ranking** module

### 2. Audited the TF-IDF Stage
- Carefully analyzed:
  - `verb_ranking/tf_idfize.py`
  - `verb_ranking/tfidf.py`
- Discovered that `tf_idfize.py` filters tokens using a **hard-coded Italian stopword list**

### 3. Verified Multilingual Infrastructure
Confirmed that the project already provides full multilingual stopword support via:
- `lib/stopwords.py`
- `resources/stop-words/` (multiple languages)

However, the TF-IDF stage **bypasses this system entirely**.

### 4. Identified a Real Architectural Issue
Because DBpedia is multilingual and the pipeline can process corpora in different languages, the current TF-IDF behavior causes:
- Silent quality degradation on non-Italian datasets
- Incorrect TF-IDF rankings
- Reduced downstream extraction accuracy

### 5. Proposed a Concrete Improvement
**Goal:**  
Make TF-IDF ranking consistent with the rest of the multilingual pipeline.

**Proposed changes:**
- Remove the hard-coded Italian STOPWORDS from `tf_idfize.py`
- Add a `--language` option to the CLI
- Load stopwords dynamically using:
  ```python
  StopWords.words(language)
### 6. Opened an Official GitHub Issue

Created a detailed issue with technical explanation and proposed fix:

🔗 Issue #94 — DBpedia fact-extractor
https://github.com/dbpedia/fact-extractor/issues/94

Also commented on the issue offering to implement the fix if the maintainers agree.

### Key Learnings

- Learned to audit production research code critically

- Identified a real architectural flaw in a live open-source project

- Practiced professional issue reporting and community communication
