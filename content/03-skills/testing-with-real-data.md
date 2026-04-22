---
title: "Testing with Real Data (Not Mocks)"
created: 2026-04-14T10:05:00Z
modified: 2026-04-14T10:05:00Z
type: skill
retention: permanent
status: active
tags: ["#type/skill", "#topic/testing", "#topic/code-quality", "#domain/development"]
summary: "Test-driven development must use real data sources, not synthetic mocks that hide actual integration failures."
sources: ["memory/feedback_testing_mocking.md"]
provenance:
  extracted: 1.0
  inferred: 0.0
  ambiguous: 0.0
---

# Testing with Real Data (Not Mocks)

## Rule

Never mock external data sources or pipeline outputs. Always use real data flowing through the system.

## Why

In the SLR (Systematic Literature Review) pipeline, synthetic checkpoints and mock extraction templates masked the fact that the extraction stage was returning empty/null fields. Tests passed with synthetic data, but the report was unreadable placeholder text. Real pipeline execution exposed the issue immediately. Mocks created false confidence about correctness.

## How to Apply

- **Multi-stage pipelines**: Run end-to-end with real data from external APIs
- **Checkpoint/resume logic**: Always save and reload real data to verify persistence works
- **Data extraction**: Never seed checkpoints with template examples—only save actual results
- **SLR components**: Integration test against real API responses (even cached), not synthetic mocks
- **Checkpoint files**: Should contain real extraction results, not example JSON

## Related Incident

- SLR extraction stage was writing synthetic/template data (269 identical records with sub_question_relevance=2)
- Quality assessor output keys didn't match orchestrator expectations (silent failure)
- Report generator had placeholder text "[Findings synthesised...]" because extraction fields were null
- All caught immediately when running real pipeline; would have passed any mocked unit tests

## Principle

Tests that pass with mocks but fail with real data are worse than no tests. Prioritise end-to-end validation with real sources.

## Related Skills

- [[07-Wiki/03-skills/code-quality|Code Quality Standards]]
- [[07-Wiki/03-skills/slr-pipeline|SLR Pipeline Development]]
