@"
## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/156

**Issue title:** README scorer test fixture is too short for its own word-count assertion

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The test_readme_with_all_quality_signals test in tests/unit/test_readme_scorer.py checks that a README with strong quality signals scores as "comprehensive," which requires a word count over 100. However, the fixture README used in the test only contains about 51 words, so the assertion word_count > 100 fails even though the scorer itself is working correctly. This is a test data bug, not a bug in the scorer logic. A successful fix will either extend the fixture README's content so it genuinely exceeds 100 words and qualifies as "comprehensive," or adjust the assertion to match realistic fixture length.

**Branch name:** fix/156-readme-scorer-test-fixture-word-count

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

**Issue selection checklist reasoning:**

- **Understanding:** The test test_readme_with_all_quality_signals in tests/unit/test_readme_scorer.py asserts a fixture README scores word_count_category == "comprehensive," but the scorer (agent/tools/readme_scorer.py) defines "comprehensive" as 500+ words. The fixture only has ~51 words, so it fails well before even reaching the "adequate" threshold (100-499 words), let alone "comprehensive." This is a mismatch between the fixture and the category thresholds it's meant to validate, not a bug in the scorer logic itself.
- **Affected area:** tests/unit/test_readme_scorer.py (test) and agent/tools/readme_scorer.py (scorer being tested). Confirmed both files exist and read the full test function plus the _score_readme method's category logic.
- **Definition of done:** Before the fix, the test fails on assert 51 > 100. A correct fix has two possible paths: (1) extend the fixture README to genuinely exceed 500 words so it legitimately earns "comprehensive," matching the test's original intent to validate a top-tier README, or (2) keep the fixture short and change the expected category to "adequate" to match realistic ~100-150 word content. I'll pick whichever better matches what the test is actually trying to demonstrate.
- **Tier fit:** First open-source contribution, so choosing Tier 1 intentionally. The fix is localized to one test file (and possibly a fixture string), matching Tier 1's "broken test" description.
- **Codebase readiness:** Read the full test class and the _score_readme method, including the word-count categorization logic and all quality-signal checks (installation, usage, badges, demo link, tech stack). Can sketch the fix without further research.
- **Claims/competition:** I found an open PR (#164) from an external contributor claiming to fix this issue by extending the fixture to >100 words. However, on inspection, this doesn't fully align with the scorer's actual logic, which requires 500+ words for the "comprehensive" category, so their fix may only get the fixture to "adequate," not resolve the original assertion. Per the checklist, claims are non-exclusive and grading is based on my own artifacts, so I'm proceeding with my own solution.
- **Time estimate:** Small, focused fix, either extending fixture text or adjusting one assertion, plus confirming other quality-signal assertions still pass. Estimate 1-2 hours, comfortably within Tier 1's 3-6 hour range.
- **Blockers:** No open blockers referenced on the issue.
"@ | Out-File -FilePath JOURNAL.md -Encoding utf8