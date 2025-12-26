# GSoC Preparation Log — Day 1
## Day 1 — 26 Dec 2025


## Project: DBpedia — fact-extractor

### Summary
Today I made my first real open-source contribution to the DBpedia `fact-extractor` project.

### Work Completed
- Explored the DBpedia organization and selected `fact-extractor`.
- Identified Issue #88 related to hardcoded Italian stopwords.
- Understood the pipeline and the role of stopword filtering in `produce_labeled_data.py`.
- Forked the repository and created a feature branch `fix-stopwords-language`.
- Implemented a fix to:
  - Remove hardcoded Italian stopwords.
  - Introduce a CLI parameter `--language` for stopword selection.
- Opened Pull Request #93 to the upstream repository.
- Responded to automated CodeRabbit review feedback.
- Fixed a critical runtime bug by passing the `language` parameter into `main()` properly.
- Pushed the fix and verified that all checks are passing.
- Communicated completion via PR comment.

### Skills Practiced
- Reading and understanding large codebases
- CLI design with Click
- GitHub workflow: fork → branch → commit → PR → review → fix → update
- Responding to automated code reviews

### Result
Pull Request is open, clean, and ready for maintainer merge.

---

### Next Steps
Wait for maintainer feedback and continue contributing.
