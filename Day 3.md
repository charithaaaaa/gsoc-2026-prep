
### Day 3 — Pipeline Stabilization & Bug Validation

### Objective

* Make the DBpedia fact-extractor pipeline runnable on a modern system
* Validate the multilingual TF-IDF issue (Issue #94) with real execution

---

### Work Completed

#### 1. Environment & Compatibility Fixes

* Identified that the codebase was written for Python 2 and fails on modern Python
* Installed Python 3.9 and created a clean virtual environment
* Fixed runtime compatibility issues:

  * Replaced deprecated syntax:

    * `ur'...'` → `r'...'`
    * `dict.has_key()` → `k in dict`
* Installed missing dependencies (`click`, `numpy`)
* Worked around legacy dependency failure (`rdflib 4.2.0`) using a compatible setup
* Configured environment so all imports resolved correctly

#### 2. Pipeline Execution

* Successfully executed the TF-IDF ranking stage:

  ```
  python verb_ranking/tf_idfize.py verb_ranking/test_corpus verb_ranking/tokens.txt --dump-tfidf
  ```
* Generated output files:

  * `tfidf.json`
  * `variances.json`
  * `stdevs.json`
  * `threshold_rank.json`

#### 3. Bug Reproduction & Validation

* Created a bilingual test corpus (English + Italian)
* Observed TF-IDF output:

  ```json
  "is": {}
  "è": {}
  ```
* Analysis:

  * Italian stopword `è` was correctly filtered
  * English stopword `is` was not filtered
  * Confirms TF-IDF pipeline is hard-coded to Italian
  * Confirms inconsistency with DBpedia’s multilingual architecture
* This provided direct experimental evidence for Issue #94

---

### Key Learnings

* Legacy research code requires significant modernization for reproducible results
* Correct environment setup is critical before meaningful contribution
* The multilingual TF-IDF issue is real, measurable, and reproducible

---

### Next Steps (Day 4)

* Implement multilingual stopword support in `tf_idfize.py`
* Add `--language` CLI option
* Replace hard-coded Italian stopwords with DBpedia’s multilingual stopword system
* Re-run TF-IDF to validate the fix
* Open a pull request referencing Issue #94

---

