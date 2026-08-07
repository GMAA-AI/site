# GMAA Engine, Changelog

All notable changes to the GMAA engine, newest first, beginning at the initial public release. **Versions are cited on two axes, always together:** the package version (this artifact) and the canon pin (the specification version the artifact ships and conforms to). Every content change is a new version, nothing is ever rebuilt in place under an existing label. Each released version lists its integrity fingerprints; verify your download against them before use (`sha256sum` the zip, then `sha256sum -c MANIFEST.sha256` inside it).

Canonical: [gmaa.ai](https://gmaa.ai) · Repository: [github.com/gmaa-ai/gmaa](https://github.com/gmaa-ai/gmaa) · Spec licensed CC BY 4.0 · Engine source-available under PolyForm Internal Use 1.0.0 · Cite by version.

---

## v2.5.2 · canon pin v1.5, Initial release *(forthcoming; fingerprints published at release)*

The first public release of the GMAA engine: a faithful generic extraction of a live production multi-agent architecture, independently reviewed pre-release by the production program it derives from.

**In the box:**
- The complete governance machinery: lane resolution, launch, doorbell and inbox transport, sync, validation, audit hooks, standing probes, and the reaper, with per-file integrity (`MANIFEST.sha256`).
- Seven agent definitions, including the orchestrator, the dispatch executor, and the optional code-substrate architect seat.
- The portable contracts and schema slots, the operating contract, the standing disciplines with boot-creed trigger binding, and the project-foundation skeleton your architect instantiates.
- The specification (canon v1.5) at `canon/`, also published at [gmaa.ai/canon.html](https://gmaa.ai/canon.html) under CC BY 4.0.
- First-launch genesis of all runtime-born state surfaces, a fresh installation boots clean, with every guard-checked file created and stamped at first launch.
- Program-qualified session identity per spec §7.3 (`{program}-{lane}`, stamped at provisioning): multiple GMAA programs co-reside on one machine without collision, and the doorbell resolves exactly one target or halts.
- `scripts/preflight.sh`, the substrate floor (Claude Code CLI, git with GitHub access, tmux; WSL2 on Windows) made testable: pass/fail per item, loud on any miss.

**Known behavior on a fresh installation:** the orchestration-freshness probe reads STALE until your program's first decision binds, it measures orchestration life, and a newborn installation has none yet. It self-clears at the first bound decision; it is a report, not a halt.

**Companion artifacts (alongside the archive, not inside it):**
- **The Operator's Guide**, the human-side manual: the ferry, the doorbell, shutdown handshakes, restarts, and what to do when a seat halts.
