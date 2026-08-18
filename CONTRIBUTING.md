# Contributing

This repository is used for training material and cohort project specifications.

## Change rules

1. Do not silently delete or weaken an existing business requirement.
2. If a requirement is superseded, retain its identifier and document the replacement in the traceability section.
3. Separate **business requirement**, **technical design** and **implementation choice**.
4. Prefer measurable acceptance criteria over subjective wording such as "fast", "secure" or "scalable".
5. Any new external dependency must have a clear purpose and be documented.
6. Examples must never contain real credentials or customer data.
7. Major architecture changes require an ADR.
8. Update `CHANGELOG.md` for material changes.

## Pull request checklist

- [ ] Requirement IDs remain stable or are explicitly migrated.
- [ ] Markdown links work.
- [ ] Examples are sanitized.
- [ ] Security implications are considered.
- [ ] Acceptance criteria are testable.
- [ ] Documentation and diagrams match the proposed implementation.
- [ ] The change is understandable without verbal explanation.
