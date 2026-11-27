# EasyMeet AI — CI Runner

This public repository contains **CI workflows only** for the private application repository [EasyMeet_AI](https://github.com/arkaprovomajhi007-AI/EasyMeet_AI).

## Run validation

1. Add a fine-grained, read-only access token as repository secret `SOURCE_REPO_READ_TOKEN`. Grant access only to the private `EasyMeet_AI` repository and the Contents: Read-only permission.
2. Open **Actions → EasyMeet source validation → Run workflow**.
3. Select `phase1` to validate private PR #36 or `phase3` to validate private PR #35.

The workflow checks out the selected pull request merge ref from the private repository and runs frontend type-check/build, server unit and Firestore emulator tests, server type-check and server build.

No application source, provider credentials, Firebase secrets, OAuth secrets or production data belong in this repository.

## Security boundaries

- Workflow permissions are read-only.
- The private source token is used only for checkout and is not persisted in the checkout configuration.
- Do not add private application files or secrets to this public repository.
- Keep deployments, production operations and live provider acceptance in the private project workflow.

A successful CI run validates the checked-out PR merge ref only. It is not production acceptance or approval to merge/deploy.
