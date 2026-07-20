## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/156

**Issue title:** README scorer test fixture is too short for its own word-count assertion

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The test_readme_with_all_quality_signals test in tests/unit/test_readme_scorer.py checks that a README with strong quality signals scores as "comprehensive," which requires a word count over 100. However, the fixture README used in the test only contains about 51 words, so the assertion word_count > 100 fails even though the scorer itself is working correctly. This is a test data bug, not a bug in the scorer logic. A successful fix will either extend the fixture README's content so it genuinely exceeds 100 words and qualifies as "comprehensive," or adjust the assertion to match realistic fixture length.

**Branch name:** fix/156-readme-scorer-test-fixture-word-count

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger
