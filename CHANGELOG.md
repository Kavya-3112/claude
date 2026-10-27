# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

This project is under Git version control (branch `feature/initial-implementation`, two commits as of this entry) but has not been released or tagged; the version number below (`0.1.0`) is taken as-is from `package.json` because it is the obvious candidate, not because a release has occurred. No release date is recorded for a version; only the date this entry was written is given.

## [Unreleased] - entry written 2026-10-27 (regenerated; supersedes the entry previously committed in `27186ee`, which was deleted from the working tree before this rewrite)

### Added

- Initial implementation of a client-only contact management web app: add, view, edit, delete, and search contacts by name or phone number, with no backend, accounts, or network calls at runtime.
- Local persistence to the browser's `localStorage`, including schema validation of stored data, salvage/recovery handling for unreadable (corrupted) stored data with explicit user confirmation before any replacement, and a leftover-backup restore/discard flow.
- A save-status banner that reports failed saves (for example, storage quota exceeded, or storage unavailable/private-browsing "memory-only" mode) with a Retry action.
- Cross-tab awareness: a tab detects when another tab has changed the underlying stored data and offers a safe reload prompt rather than silently overwriting newer data.
- Search by name (case-insensitive substring) and by phone number (formatting-insensitive, ignoring a leading `+`).
- A build-time Content-Security-Policy, injected into the production build only, confirmed present in the built `index.html` (re-confirmed 2026-10-27, byte-identical to the 2026-10-23 build output).
- `README.md` with install, development-server, production-build-and-serve, and test instructions, plus documented storage, security, and deployment caveats.
- `traceability-matrix.md` mapping all 57 functional requirements and 11 non-functional requirements to their covering tests (or to a named, honest gap where no test exists).
- `accessibility-assessment.md` documenting automated accessibility results (axe-core, 0 violations across every required view/state under both a Chromium and a Firefox Playwright engine) and genuine keyboard-only operability tests, while explicitly stating that manual assistive-technology testing (NVDA + Firefox) could not be performed in the build environment and is not claimed.
- Both a `firefox` and a `chromium` Playwright project are configured (`playwright.config.ts`), giving the e2e suite automated cross-engine coverage beyond Chromium alone.

### Known limitations

- No WCAG 2.2 AA conformance claim is made. Automated accessibility checks are clean under both configured Playwright engines, but manual assistive-technology testing has never been performed on this application (blocked: no NVDA or desktop Firefox installation available in the build environment).
- Two Playwright end-to-end tests fail only under the Firefox test engine (`tests/e2e/recovery.spec.ts` "copy puts the exact original on the clipboard" and `tests/e2e/csp.spec.ts` "...Blob download and copy work... under the CSP with no violations"), both with `browserContext.grantPermissions: Unknown permission: clipboard-read`. This has been independently reproduced 6/6 across isolated re-runs on two separate occasions (2026-10-23 and 2026-10-27) and is assessed as a Playwright-Firefox automation-driver limitation (the driver does not recognize the `clipboard-read`/`clipboard-write` permission names Chromium accepts), not an application defect. **Disposition: UNVERIFIED-BY-THIS-ORCHESTRATOR** — no directly-verified user decision to accept, fix, or skip these two tests exists as of this entry; they are left failing, not skipped or deleted, as an honest, visible record.
- No scale/load test exists for larger contact lists (a few hundred contacts, NFR-11). The underlying gap is confirmed genuinely absent from the test suite. **Disposition: UNVERIFIED-BY-THIS-ORCHESTRATOR.**
- A small number of narrow, low-severity findings around mutation-blocked UI states are documented but not fixed: CR-13 (MEDIUM, an untested-by-execution cross-tab backup interaction, traced by code-reading only) and CR-17 (LOW, the delete-confirmation dialog's action button is not reactively disabled if a mutation block newly appears while the dialog is already open; the store-level guard still prevents the actual mutation, so this is a UX-only gap). **Disposition for both: UNVERIFIED-BY-THIS-ORCHESTRATOR.**
- No hosting provider has been chosen and no deployment or CI configuration exists in this repository; only local build/serve/test instructions are provided.
- A host-delivered Content-Security-Policy response header and a dedicated `innerHTML`-usage audit remain outstanding; only the build-time CSP `<meta>` tag mechanism is implemented and tested.
- `npm audit` reported 0 vulnerabilities on 2026-10-23; a 2026-10-27 re-run could not reach the npm registry in that environment (`EAI_AGAIN`, no outbound network/DNS access) and neither confirmed nor contradicted that result. Current dependency/vulnerability status should be treated as last verified 2026-10-23, not as freshly re-verified.
- The approval status of `requirements.md`, `architecture.md`, `design-review.md`, and `impl-plan.md` (Stages 1-4) remains recorded as **PROPOSED, approval UNVERIFIED by the orchestrator** — see `.github/sdlc-status.md`. This is an open governance item, not a code defect.
