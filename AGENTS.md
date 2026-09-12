# Markpad agent instructions

## Editor and native contracts

- Preserve users' document contents, unsaved edits, file identity, and open/reload/export behavior. A failed write or cancelled dialog must not be reported as a successful save.
- Runtime file operations go through Rust/Tauri commands, not Node filesystem APIs in the browser. Keep command arguments, results, errors, and frontend consumers compatible.
- Keep Svelte 5 runes-based state and existing shared stores/components. Match the repository's tab indentation and TypeScript conventions without introducing a parallel framework or broad formatting churn.
- Treat Markdown, frontmatter, embedded HTML, paths, and external content as untrusted. Preserve sanitization and deliberate opener behavior in previews/exports.
- Never modify `plugins.updater.pubkey` in `src-tauri/tauri.conf.json`. Updater trust material is maintainer-controlled, not a repair knob.
- Version changes must update `package.json` and `src-tauri/Cargo.toml` together in the same commit, with corresponding lockfile changes when required. Preserve frontend/native/updater version agreement.

## Guidance and verification

Use [package.json](package.json) for actual frontend checks: `npm run check`, the relevant `test:frontmatter`, `test:workflows`, or `test:settings-scroll` script, and `npm run build` when affected. Do not assume frontend tests are absent. Native checks are scoped in `src-tauri/AGENTS.md`.

Use [RELEASING.md](RELEASING.md) only for packaging/update/release work. Preserve committed dependency locks, target-specific behavior, and signing prerequisites. Installer mode, personal documents, and live updater endpoints are not routine test fixtures.

Completion requires the changed editor/native contracts exercised with disposable files, relevant checks recorded, and documentation synchronized. A web build does not prove a packaged Tauri application or an update works on every supported OS.
