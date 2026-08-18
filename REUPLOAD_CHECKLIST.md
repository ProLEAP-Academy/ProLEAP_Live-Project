# Re-upload Checklist

Use this when replacing the old GitHub repository contents with the modernized pack.

## Before upload

- [ ] Keep a tag/branch/archive of the old repository.
- [ ] Review `docs/09-modernization-and-traceability.md`.
- [ ] Confirm whether you want the repository public or private.
- [ ] Confirm the repository description and topics.
- [ ] Decide whether `legacy/` should remain visible to learners or only maintainers.

## Upload / replace

- [ ] Replace the old root README with this repository's `README.md`.
- [ ] Upload `docs/`, `projects/`, `templates/`, `.github/`, `exports/` and root governance files.
- [ ] Keep `.gitignore` and `.editorconfig` at repository root.
- [ ] Commit the `legacy/` directory in the migration release if historical traceability is desired.
- [ ] Use a release/tag such as `v2.0.0` for the first modernized revision.

## GitHub settings to consider

- [ ] Protect `main` if multiple maintainers contribute.
- [ ] Require pull requests for specification changes.
- [ ] Enable secret scanning/security features available to the repository plan.
- [ ] Enable Issues if learners will use the provided issue templates.
- [ ] Add repository topics such as `devops`, `cloud`, `platform-engineering`, `observability`, `devsecops`, `live-project`.

## After upload

- [ ] Click every main README project link.
- [ ] Confirm Mermaid diagrams render.
- [ ] Open each PDF under `exports/`.
- [ ] Verify no dataset, credential or private key was accidentally uploaded.
- [ ] Create a test issue from each issue template.
- [ ] Create one test pull request and verify the PR template.
- [ ] Publish a short release note summarizing the v2 modernization.
