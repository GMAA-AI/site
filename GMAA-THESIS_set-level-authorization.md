# The Coherence Boundary
### Why governed multi-agent systems must authorize the *set*, and not only the change

*A GMAA position paper. Canonical: [gmaa.ai](https://gmaa.ai) · cite by version.*

> **What this argues, and what it doesn't.** GMAA is governance for multi-agent software work — it governs *each* change and *the set* those changes form. This paper is about the second unit: the claim that the complete pending set must be authorized as a whole, which no shipping system or published protocol does. It proves that claim is distinct, and defends why the human at its center is load-bearing rather than legacy. It does **not** claim that any built system already surfaces the *complete* set of conflicts — that has to be earned against an adversarial test, not asserted. The line between what is established and what is still open is drawn explicitly at the end, and holding it is the point.

---

## 1 · The claim, in one sentence 

At the single point where changes enter a system of record, the unit that must be authorized is **not only each change, but the complete set of pending changes — evaluated together against the invariants of that system, ratified as a set by an accountable human independent of every initiator, before any member of the set commits** — with a receipt trail as the audit evidence.

The load-bearing word is **set**. It is the unit that gets governed *in addition to* each change — not instead of it. Per-change governance stays; the set is the layer that was missing.

## 2 · What the claim is not

Each of these is a real, capable mechanism. The claim is precise about which one it is — and which it isn't.

- **Not multi-agent orchestration.** Running twenty or thirty agents in parallel against one repo is a solved operability problem, implemented in open source. This claim is not about making agents *run*; it's about what gets *authorized*.
- **Not "a single writer avoids conflicts."** Single-writer-as-the-only-way is disproven, not merely unproven: peer-reviewed protocols keep full concurrency and prove serializability at quiescence via speculative writes and saga-style undo (CoAgent/MTPO). The claim does not rest on single-writer being the only route to safety.
- **Not "coherence beats serializability."** That argument is contestable, and the claim no longer needs it. Serializability guarantees equivalence to *some* serial order; it is agnostic to domain invariants. Even granting maximum overlap, the claim survives on a different axis (§3).
- **Not per-change segregation of duties *alone*.** Per-change SoD is necessary, and GMAA runs it — the initiator of each change is never its authorizer. But per-change SoD is not *sufficient*: answer it correctly, three times, with proper independence, and an incoherent aggregate still commits. The set is a **second** unit of authorization the claim adds; it does not remove the first.
- **Not a different category from AI governance — a different *unit* within it.** Per-action governance platforms already route each agent action through its own approval chain with per-agent identity and audit. That is real governance, and it is useful. It governs the **action**. GMAA governs the change *and* the set. The distinction is the unit, not the category: GMAA is the governance that also covers the set, which the per-action layer never reaches.

## 3 · The load-bearing distinction: everyone governs *a* unit; only one governs the set

Every adjacent mechanism authorizes, resolves, or reviews at *some* unit — and each does its unit correctly. The gap is that the failure that matters does not live at their unit.

An authorizer who approves change A, then B, then C — each in isolation, each correctly, each with proper independence — has satisfied per-change authorization and segregation of duties completely, and has still never seen the thing that breaks. The break does not live in A, or B, or C. It lives in **{A, B, C}** as a set: three individually valid, individually permitted, individually approved changes whose interaction violates an invariant of the system of record. The per-change approvals were not *wrong* — they were **incomplete**. There was a second unit, the commit set, and nothing was scoped to govern it.

That is why the claim does not depend on winning the coherence-versus-serializability argument. Serializability operates on the set but removes the human. Per-change authorization keeps the human but stops at the change. Neither supplies **set-level authorization by an independent human before commit**. That intersection is empty — and it is where GMAA adds a unit, on top of the per-change governance it already runs.

**The honest complement, stated plainly:** member-level checks remain necessary. GMAA does not relax them — it depends on them. Every change still passes its own verification, its own gate, its own receipt. The boundary's argument is only that those checks are not *sufficient*, because a set of individually-passing changes can still be jointly incoherent. Set-level authorization is the completion of member-level governance, not a replacement for it.

## 4 · The cell of one

Four properties define the ground for the *set*. The claim is that only one arrangement holds all four at once — and that the same arrangement also keeps the member-level governance the others do.

| | Unit reviewed | Independent human authorizer | Against domain invariants | Before commit |
|---|---|---|---|---|
| **Serializable multi-agent concurrency control** (e.g. CoAgent / MTPO) | the set (for serializability) | **no** — the notification goes to the agent, which self-heals; the human is designed out | no — serializability only | at quiescence, auto-repaired |
| **Per-action AI governance** (e.g. per-agent approval chains + audit) | **the individual action** | yes (approval chains) | policy per action, not joint | per action |
| **Per-change SoD / classic IT change control** | the individual change | yes (independent approver) | per change | per change |
| **GMAA — governance at the coherence boundary** | **each change *and* the complete set** | **yes — an independent accountable human** | **the joint invariants of the system of record** | **before any member commits** |

Only the last row holds all four columns for the set — *and* it is the only row that also keeps per-change governance. The concurrency protocol governs the set but removes the human. The per-action and per-change controls keep the human but govern only their single unit. GMAA governs the change and the set. From what a careful survey can find, that combination is a cell of one. ("Nobody does this" is impossible to prove and easy to break with a single example; the claim is stated precisely so it can be tested, not so it can hide.)

## 5 · Two worked cases

**A software case — the shape of the failure.** A system of record has a rule: a column's name is defined in exactly one place, and every reader uses that name. Three agents, three branches, three independently-passing changes: one renames the column; a second adds a query that still expects the old name; a third adds code that assumes both exist during a transition. Each passes its own tests. Each is individually correct — and correctly governed at the member level. Jointly, the set leaves the system referring to a name that no longer resolves the way any single change assumed. No reviewer saw `{A, B, C}` together. The defect exists only in the combination, so no amount of per-change care finds it.

**A regulated case — why it's a named deficiency.** Replace the codebase with a general ledger, a financially material system of record under SOX Section 404. Same shape:

- **Change A** (data-platform lane, data-eng lead approves): remaps a node in the account hierarchy. Valid alone. Independently approved.
- **Change B** (application lane, app owner approves): changes a posting or allocation rule that references an account code. Valid alone. Independently approved.
- **Change C** (finance-config lane, finance-systems owner approves): updates a consolidation or tax mapping that references the same account. Valid alone. Independently approved.

Each clears per-change segregation of duties — the initiator is not the authorizer; an independent party signed each one. Jointly, A's remap plus B's posting rule plus C's consolidation route an amount twice, or into the wrong period, or into the wrong classification. The result is a **material misstatement** of the financial statements. No single approver saw the set. Per-change authorization passed three times. The aggregate is the control gap.

## 6 · The SOX mapping: a named deficiency, not a nice-to-have

On the framework text:

- **Change authorization.** ITGC expects formal, multi-level approval for all system changes. As implemented across the industry, this is per change.
- **Segregation of duties.** No single individual has end-to-end authority over a transaction; responsibilities divide across initiation, authorization, and reconciliation. As implemented, this is per change.
- **The canonical failure.** Developers with direct access to deploy changes into production financial systems is a documented separation-of-duties violation and a **Section 404 material weakness**; the accepted remediation is that production changes require explicit approval by someone other than the initiator, through a trusted pipeline.

The deficiency the aggregate case exposes: both objectives are satisfied *per change*, and the material misstatement still commits — because the change was governed and the set was not. Three correctly authorized changes produce an unauthorized joint state, and no per-change control is scoped to see it.

Set-level authorization is the compensating control that completes the others. It adds the commit set as a unit: assemble the complete set of pending changes to the material system of record at one coherence boundary, surface the joint impact against the system's invariants, and require one accountable authorizer — independent of every initiator — to ratify the set before any member commits, with the receipt trail as audit evidence. That maps directly onto change authorization and SoD, at the granularity the failure actually lives at, without giving up the per-change granularity underneath it.

## 7 · The boundary produces a briefing, not a verdict

Set-level authorization answers "may this set commit." But a change authority does not only approve or reject — it *deliberates*, and deliberation needs both the conflict surfaced *and* a set of moves it can actually make. A boundary that only says "these three are jointly incoherent, halt" hands the forum a problem with no options and sends every lane back to renegotiate blind. So the boundary's second output, alongside the complete conflict surface, is the complete set of grounded resolution paths, each with its cost.

The moves against a jointly-incoherent set are a small, bounded taxonomy — naming it is what makes the function buildable rather than a vague "suggest alternatives":

- **Sequence.** The conflict is order-dependent; commit A before C and it dissolves. The cheapest move, and often available, because many aggregate conflicts are ordering artifacts. (One-at-a-time commit destroys this move retroactively: by the time member N exposes the break, 1…N-1 are already committed and unreorderable — which is *why* the set must be seen before any member lands.)
- **Scope.** Narrow one change so it stops touching the shared invariant, keeping its intent.
- **Hold.** Commit the coherent subset now; defer the conflicting member to a named later window under a stated condition.
- **Substitute.** A different change achieves the same intent without the collision.
- **Reject and escalate.** The conflict is existential — incompatible intents, unsaved by any ordering or scoping. A human with authority must decide which intent wins.

Sequence and reject-escalate are the floor and ceiling; everything useful sits between.

## 8 · Why the human is a boundary, not a bottleneck

The strongest objection to keeping a human here is clean: modern practice spent a decade automating away per-change approval because the human forum was a throughput bottleneck; frameworks now expressly permit automated controls when the underlying general controls are effective. So — the skeptic says — build a trusted, independent automated authority that detects the complete conflict set, computes the options, and authorizes the chosen one, and the human is just the next bottleneck to remove.

The defense has two grounds. The first is real but does not close the objection; the second does.

**Accountability (necessary, not sufficient).** An automated authority that shares the initiators' substrate, provenance, and failure modes is not independent in the sense segregation of duties means — it can carry the exact blind spot that produced the incoherence, the way a module cannot audit itself. That argues for separation. It does not defeat the objection, because a genuinely *separate* automation — different provenance, different operator — could claim the independence the rule asks for. Conceding this is what keeps the argument honest. The claim does not stand here.

**The deciding facts are outside the machine's input space (the closer).** The correct resolution of a jointly-incoherent set is frequently *not* determined by the system of record. Which move is right — sequence versus hold versus reject — can turn on a fact that exists only in organizational and strategic knowledge and is nowhere in the store: a datacenter cutover next quarter, a decision to sunset the stack the change targets, an M&A event, a vendor exit, a customer commitment, a regulatory deadline not yet encoded as data. An automated authority, however trusted and however independent, cannot select an option that references a fact it has no channel to read. This is not a maturity gap a better model closes; it is a category boundary — the automation's input space is the system of record, and the deciding fact lies outside it.

So the division is not human-versus-automation; it is **briefing, then authorization**. The automation produces the briefing — the complete conflict set and the grounded option set. The human authorizes — extending the option set with the out-of-band facts, then selecting. The authorization seat is human because that seat is *where the out-of-band facts enter*. You cannot automate access to a fact that exists only in a decision not yet taken. That is exactly why the frameworks, having automated everything they could, kept human review for "high-impact changes and important organizational concerns and cross-team coordination." That residue is the set-level coherence decision. The industry named the boundary; this argument says why it cannot move.

There is an honest scope limit: this proves necessity for the subclass of sets whose resolution turns on out-of-band context, not for *every* set. A set fully determined by the system of record could in principle be authorized by a sufficiently trusted independent automation. Two things keep the human the default anyway. First, the high-stakes sets are disproportionately the context-entangled ones. Second, and decisively: no one can know in advance that a given set is context-free without a human confirming no out-of-band constraint applies — and that confirmation *is* the authorization. The machine cannot certify the absence of a fact it cannot see.

## 9 · What's established, and what the field shows, and what's still open

**Established.** The claim occupies ground no shipping system or published protocol occupies — proven on regulatory ground rather than on the contested coherence-versus-serializability argument. Serializable concurrency control governs the set without a human; per-action and per-change governance keep an independent human at their single unit. None governs the set with an independent human before commit — which is exactly what a SOX-scoped system of record requires and does not get from per-change controls. And the human at that seat is load-bearing by construction, because it is the only party holding the out-of-band input.

**What the field shows.** These claims are not only argued; a running governed multi-agent deployment has exercised them, and the patterns are worth stating (as existence, not as completeness):

- **The failure mode is real and was caught in the reference system itself.** In live operation, per-change review ran correctly at every seat while a multi-member pending set accumulated *unevaluated* — the exact gap this paper describes, occurring in a system that had not yet instrumented the boundary. Naming it is what turned it from an invisible risk into a governed one.
- **Member-level and set-level governance are complementary, and both fire.** Individually-passing changes have been surfaced as jointly incoherent before any of them committed — a change and a build that each passed alone but contradicted each other once a third landed — halted at the boundary, at zero cost to the substrate. Per-change governance did its job; the set-level layer caught what per-change cannot.
- **Governance concentrates nowhere — including the seats that author the rules.** The mechanism has caught its *own* governors: a rule-author citing a rule that was never actually filed, and a governance record composed from a stale copy of itself — each caught before it could propagate. "Nobody signs their own work" held even for the authoring seat.
- **The shape is what systems converge on under real pressure.** Independent product builds have arrived at the set-level ratification surface on their own, without a mandate to — because member-at-a-time approval kept producing the exact defect the claim predicts, including the observation, stated in the field, that *a ratification surface that can only say yes is a rubber stamp by construction.*

**Open — and not claimed until earned.** Does a given implementation surface the *complete* set of joint incoherences, including transitive conflicts and conflicts through a shared unforkable artifact? And does it produce a *complete, sound* option set — never proposing a resolution that can't actually resolve, never missing the one that matters? These are earned with an adversarial miss-hunt that tries to find the class the boundary misses — by planting problems you already know about and owning the ones your system doesn't catch. An integrator that catches most joint incoherence but misses a class is a linter, not the control. Completeness is not asserted here. No fake closures.

That distinction is the whole discipline. The shape of the control is proven, and the field shows it governing real sets. Whether any particular build catches *every* incoherence is a separate question, and the trust position depends on not claiming the second until it's earned.

## 10 · Honest edges

- **Frameworks permit automated controls.** This is the strongest objection, addressed in §8: it can contest the accountability ground but not the out-of-band-context ground, so it does not close the human out of the reserved class.
- **This ties the argument to systems of record with real invariants — sharpest where those invariants are financial and audited.** That's a feature: a system of record with a compliance budget, a named risk owner, and a forcing function is where the wrong-unit failure has consequences someone is accountable for. The general "any shared state" framing is weaker precisely because it has no forcing function behind it.
- **The operational design of the boundary is a separate open problem, one layer below this claim.** Proving the set-level control distinct and its human authorizer necessary does not settle how to make that boundary *workable* at real agent concurrency. Three questions stay open there, and they belong to operation rather than to the claim: the latency of assembling and briefing the complete pending set, the threshold that decides which systems of record are "material" enough to warrant a set-level seat, and the design of that seat so it stays a boundary rather than becoming a single point of delay or a concentration of power. This is distinct from the completeness problem in §9 — completeness asks whether the conflict surface is *whole*; this asks whether the control is *practical* — and neither is claimed solved here. The shape of the control is what this paper establishes; making it run in a real environment is the work below it.

## Sources (verified 2026-08-05)

- **CoAgent / MTPO** — *CoAgent: Concurrency Control for Multi-Agent Systems*, arXiv:2606.15376 (Jun 2026). Serializability at quiescence via speculative writes and saga-style undo; the re-judge notification is delivered to the agent; the human is not in the commit path.
- **Per-action AI governance** — ServiceNow Action Fabric / AI Control Tower, announced at Knowledge 2026 (May 2026): every action routed through per-agent identity, permission scope, and audit; the unit of approval is the action; AI Control Tower offered free for one year.
- **SOX ITGC / PCAOB** — change-authorization and segregation-of-duties control objectives, and the developer-direct-to-production material-weakness pattern with trusted-pipeline remediation. Amendments to AS 2201 (*Internal Control Over Financial Reporting*) and AS 2101 (*Audit Planning*) effective December 15, 2026 (PCAOB Release No. 2024-005; SEC Release No. 34-100968).
- **ITIL 4 change enablement** — the CAB de-emphasized as a throughput bottleneck and replaced by risk-based change authorities; low-risk changes automated or bypassed; human review reserved for high-impact changes and important organizational concerns / cross-team coordination.

---

*GMAA governs each change and the set they form. The set-level control is proven distinct, the human at its center proven necessary for the class that matters, and the field shows it governing real sets — while completeness of any given build remains to be earned, and this paper does not claim it. GMAA · [gmaa.ai](https://gmaa.ai) · cite by version.*
