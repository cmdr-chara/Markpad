# Native editor agent instructions

- Keep file operations authoritative here and expose fallible Tauri commands with the existing `Result<T, String>` contract. Propagate meaningful errors to the UI rather than panicking or masking unsuccessful writes.
- Coordinate command changes with their TypeScript callers. Preserve file identity, encoding/content, cancellation, and save/reload/export semantics using disposable fixtures.
- Keep platform-specific behavior behind explicit conditional compilation and test the affected platform where required. Linux checks do not establish Windows/macOS installer or opener behavior.
- Never change the updater public key, bypass update verification, or weaken signing requirements. Root package/Cargo version synchronization remains mandatory for intentional version changes.

From this directory, run the relevant `cargo test`, `cargo check`, `cargo clippy`, and `cargo fmt -- --check` checks. Select focused tests during iteration and preserve the committed lockfile. Use [RELEASING.md](../RELEASING.md) for packaging/update work. Do not use personal documents, live installation directories, or production updater state for automatic tests.
