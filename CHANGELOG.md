# GMAA Engine Changelog

All notable changes to the GMAA engine, newest first, beginning at the initial public release. **Versions are cited on two axes, always together:** the package version (this artifact) and the canon pin (the specification version the artifact ships and conforms to). Every content change is a new version. Nothing is ever rebuilt in place under an existing label. Each released version lists its integrity fingerprints; verify your download against them before use (`sha256sum` the zip, then `sha256sum -c MANIFEST.sha256` inside it).

Canonical: [gmaa.ai](https://gmaa.ai) · Repository: [github.com/gmaa-ai/gmaa](https://github.com/gmaa-ai/gmaa) · Spec licensed CC BY 4.0 · Engine source-available under the Apache License 2.0 with the Commons Clause · Cite by version.

---

## v2.5.3 · 2026-08-09 · canon pin v1.5

**What changed:**

- **Restored the adopter-facing entry documents** that were dropped when the package was reframed from "evaluation package" to "engine" at v2.5.0 and then shipped missing through v2.5.1 and v2.5.2. That is a regression in a governance product whose whole claim is completeness. `ADOPTION-COVER.md` is back (the read-first four-phase adoption flow: fit assessment, then your adoption gate, then instantiation fills, then implementation, with the steps-you-decide split and the non-skippable step-8 proof), and `GETTING-STARTED-LINUX-MAC.md` is back (the zero-to-running walkthrough). Both are modernized to the engine: canon v1.5, `launch-orc.sh`, folder-equals-lane (the `foundation` folder, with `main` as a branch), and Phase-3 output of `docs/FOUNDATION.md` plus `seats.yaml` (the settled instantiation fills, replacing the earlier fill-template). The README now points at the cover as read-first, states that the instantiation runbook is the canon's own §12 checklist (not a shipped file), and states that instantiation follows the canon to the letter.
- **Folder-equals-lane launcher fix.** The foundation lane's worktree folder is `foundation`, uniformly with every other lane; `main` is the git trunk branch only, never a folder name. Removed the `main`-as-folder special case from `launch-orc.sh` and `scripts/orc-up.sh` so no shipped surface teaches the old convention against the docs (which say `foundation`). The `main` branch itself (`git show main:`, the worktree checked out to `main`, merge-to-main) is untouched.
- **Orchestrator agent-def loadability.** `.claude/agents/orc.md` now leads with its YAML frontmatter (a note block had preceded it), so `claude --agent orc` binds the governed orchestrator instead of silently falling back to the ungoverned default. `scripts/preflight.sh` now asserts every agent def's frontmatter leads its file.

**Files touched:** `ADOPTION-COVER.md` (restored) · `GETTING-STARTED-LINUX-MAC.md` (restored) · `README.md` · `CHANGELOG.md` (restored) · `launch-orc.sh` · `scripts/orc-up.sh` · `.claude/agents/orc.md` · `scripts/preflight.sh` · `agents/auditor-contract.md` (comment) · `CITATION.cff` · `MANIFEST.sha256`

**If you have already adopted:** add `ADOPTION-COVER.md` and `GETTING-STARTED-LINUX-MAC.md` to your package copy and replace `README.md`. If your integrator worktree folder is named `main`, rename it to `foundation` (folder-equals-lane); the `main` branch is unchanged. All are app-side files, none generated. Your generated governance files are untouched.

**Deferred to a future release:** the Windows and WSL getting-started guide.

**Prevention:** `MANIFEST.sha256` and the seal check now assert the adopter-entry set (the cover, at least one getting-started guide, and the CHANGELOG) is present, so a genericization reframe cannot silently drop it again. This is the completeness firewall (canon §13) applied to the package itself.

---

## v2.5.2 · 2026-08-07 · canon pin v1.5 · Initial release
**Fingerprints:** zip sha256 `a3ba4117cf29c024c0019d20b04aef445c0baedd1681d1012c620d35be91a1c8` · package self-sha `bcecbd286c8d9b4b0992f2af857533cf11563bd24deeeaeec84279844574e483` · 70 files + manifest.

The first public release of the GMAA engine: a faithful generic extraction of a live production multi-agent architecture, independently reviewed pre-release by the production program it derives from.

**In the box:**
- The complete governance machinery: lane resolution, launch, doorbell and inbox transport, sync, validation, audit hooks, standing probes, and the reaper (with per-file integrity in `MANIFEST.sha256`).
- Seven agent definitions, including the orchestrator, the dispatch executor, and the optional code-substrate architect seat.
- The portable contracts and schema slots, the operating contract, the standing disciplines with boot-creed trigger binding, and the project-foundation skeleton your architect instantiates.
- The specification (canon v1.5) at `canon/`, also published at [gmaa.ai/canon.html](https://gmaa.ai/canon.html) under CC BY 4.0.
- First-launch genesis of all runtime-born state surfaces: a fresh installation boots clean, with every guard-checked file created and stamped at first launch.
- Program-qualified session identity per spec §7.3 (`{program}-{lane}`, stamped at provisioning): multiple GMAA programs co-reside on one machine without collision, and the doorbell resolves exactly one target or halts.
- `scripts/preflight.sh` makes the substrate floor (Claude Code CLI, git with GitHub access, tmux; WSL2 on Windows) testable: pass/fail per item, loud on any miss.

**Known behavior on a fresh installation:** the orchestration-freshness probe reads STALE until your program's first decision binds. It measures orchestration life, and a newborn installation has none yet. It self-clears at the first bound decision; it is a report, not a halt.

**Companion artifacts (alongside the archive, not inside it):**
- **The Operator's Guide**: the human-side manual covering the ferry, the doorbell, shutdown handshakes, restarts, and what to do when a seat halts.
