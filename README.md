# EasyMeet AI — CI Runner

This public repository contains **CI workflows only** for the private application repository [EasyMeet_AI](https://github.com/arkaprovomajhi007-AI/EasyMeet_AI). All GitHub Actions validation for EasyMeet AI is initiated and executed from this repository; do not create a parallel application CI workflow in the private source repository.

## Run validation

1. Keep the fine-grained, read-only source token in repository secret `SOURCE_REPO_READ_TOKEN`. Scope it only to the private `EasyMeet_AI` repository with Contents: Read-only permission.
2. For a manual run, open **Actions → EasyMeet source validation → Run workflow**.
3. Select `phase1`, `phase3` or `both`. The default is `both`.

The workflow checks out the selected private pull-request merge ref and runs frontend type-check/build, reproducible server dependency installation with `npm ci`, server unit and Firestore emulator tests, server type-check/build and a Docker image build for the selected source branch. A one-shot lockfile-generation job is available through the `[generate-server-lock]` push marker.

## Automatic run convention

A push to `main` in this CI repository that changes either this README or `.github/workflows/validate-source.yml` starts both Phase 1 and Phase 3 validations. After making a source-only implementation update in the private repository, the project execution process updates the **CI trigger marker** below in this README. That creates the CI-repository push event, so the latest private PR merge refs are revalidated without adding application code to this public repository.

**CI trigger marker:** `2026-11-27 — Phase 1 legacy and owner Google OAuth cleanup`

## Security boundaries

- Workflow permissions are read-only.
- The private source token is used only for checkout and is not persisted in the checkout configuration.
- Do not add private application files, provider credentials, Firebase secrets, OAuth secrets or production data to this public repository.
- Deployments, production operations and live provider acceptance remain separate release gates.

A successful CI run validates the PR merge ref checked out by that run only. It is not production acceptance or approval to merge/deploy.
