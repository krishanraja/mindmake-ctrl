---
repo: krishanraja/mm-ctrl
product: CTRL by Mindmake
as_of: 2026-10-19
head: 596a088
head_scope: North Star dates set to agent speed
lifecycle: live
production_url: https://makeyourmindup.ai
state_doc: docs/current/release-state.md
history_log: docs/history/LOG.md
truth_files: [public/.well-known/product.json]
authority_order: [executable code, database readback, deployment readback, src/router.tsx, public/.well-known/product.json, docs/current/README.md, docs/current/commercial.md, project-documentation/DECISIONS_LOG.md, subsystem references and compliance records and runbooks, dated delivery notes and prototypes and roadmaps and Git history]
steward: https://github.com/krishanraja/ai-harness/blob/main/docs/steward/RUNBOOK.md
never_publish: [any login or credential or the address of the test account, the Supabase project id, secret names such as the cron secret and the video studio export token, the old $9 and $29 prices and any annual price or discount or bundle, customer counts or revenue or conversion or retention or ROI figures, any Personal Memory or briefing or decision or Blind Spot content, a security certification not named in the compliance records]
---
# CTRL by Mindmake: where it is right now

## What it is

CTRL is a calm AI briefing and decision partner for founders and small-team CEOs building the AI-native version of their business, live at `makeyourmindup.ai` with a Free tier and a $49 a month Edge Pro tier. Make Your Mind Up is its public intake, one question at a time. Four surfaces do the work: Today (a small set of corroborated AI signals ranked against the leader's real priorities, as a short read or listen), Decide (a real call weighed against live evidence, with the judgement left to the leader), Blind Spot (one private, evidence-anchored read and one small experiment) and Memory (owner-scoped, correctable, portable context the leader can export to any AI tool). It is a Vite React app on Vercel with Supabase behind it, sharing one Supabase project with other Mindmake surfaces. The product contract is one person, one account: no seats, no admin console, no SSO, no meeting recording (`project-documentation/DECISIONS_LOG.md`, Decision 82). The repository's own docs still carry the earlier "Mindmaker" name; see "What is waiting on Krish".

## Who it is for and why it matters for Mindmake

CTRL's own buyer is the AI-active founder or small-team CEO (`public/.well-known/product.json`, `icp`). For the room_face buyer in `control-center/docs/ICP.md`, a senior leader at a PE or VC backed media, adtech, publishing or data business who is quietly behind on what is coming, CTRL is not the pitch: the `mm_ctrl_buyer` lane is parked (ICP.md, 2026-09-07). CTRL is the proof. It shows that the person offering to help them run a business on AI has built, shipped and operates a paid AI product alone, holds other people's data carefully, and writes down what broke.

Angles a writer can use without asking Krish, each with its pointer:

- **The dry run was the point.** On 2026-08-21 a backfill over 196 memory rows wanted to change exactly two, and both changes were wrong: "VP Eng" would have lost "Eng" as a surname, and the account holder's own name would have been deleted from a sentence about him. The same transform ran on the live path, so the fix went there first. After it, the applied run rewrote nothing (`CHANGELOG.md`, 2026-08-21; commit `bac02d3`).
- **A control recorded as dormant was broken.** Applying the retention schedule on 2026-08-20 exposed that production had never received the `retention_expires_at` column, so a leader changing their retention window got a database error instead of a saved setting (`docs/current/release-state.md`, "The partial migration this readback uncovered").
- **Enterprise exposure comes from the data, so the frame is held structurally.** The moment a leader voices an unannounced deal or a judgement about a colleague, the product holds confidential information. The answer was product contract, not positioning: no seats, no SSO, nothing an IT administrator has to approve (commit `962d0e8`, Decision 82).
- **The trust page names what is missing.** `/trust` lists controls in place, in progress and absent, and says there is no SOC 2 report and no ISO 27001 certificate (PR #370).

Objection it answers: "He talks about AI. Has he shipped anything a customer pays for and kept it honest?" Here is the product, with its failures in the changelog.

## Where it is right now (as of 2026-10-19)

- **Live** at `makeyourmindup.ai`. The exact G16 application release is `860dea0`, Vercel `dpl_2JFRfmZRzUvxbdwXqLunG3eubTgc`, READY and PROMOTED from that SHA (`docs/current/release-state.md`). Answer-only publishing and documentation receipts may advance `main` and create newer deployment IDs without changing this G16 receipt.
- **Edge Functions:** 116 directories in the tree (`measure-standard` restored, PR #398). 114 of the earlier 115 were confirmed deployed and ACTIVE by management API readback on 2026-08-21; `measure-standard` has no readback recorded here. `live-headlines` version 48 deployed and verified against cache readback on 2026-09-02 (476 items, 473 classified, 12 `damage` dropped). Two changes have no deployment readback recorded here: `video-radar-export` (PR #371, 2026-08-28) and the rolling-window merge (PR #375, `edd9045`).
- **Tests:** 945 tests in 60 files passed at the G16 release (`860dea0`, 2026-09-08), with zero new type errors against the 94-error legacy baseline. Later commits added Brain adapter, synthetic population and trend-memory tests, and no newer count is recorded in `docs/current/release-state.md`, so the current number is unverified. CI runs docs, standards, tests, typecheck, build and changed-file lint on every push.
- **Living Brain substrate:** 11 additive production tables are live, empty and disconnected from customer paths. Forced RLS, non-anonymous workspace membership, exact-audience grants and authenticated read-only ACLs protect them. The strict write-adapter primitives (`brain-crypto.ts`, `brain-ingest-core.ts`) exist as tested shared modules only: no function, key, workspace or row has been created (`g17-service-adapter-contract.md`). A deterministic 48-account synthetic population and an unlinked range lab at `/operator/lab/synthetic-population/:accountId` exist for development and flagged preview builds (`g18-synthetic-population-lab.md`). G20 (`g20-universal-capture-claude-bridge-contract.md`) is a founder-confirmed contract for paste-in capture and a scoped Claude bridge, with no connector or UI authorised. The writable multi-identity behavioural test remains future work (`g16-workspace-audience-canary.md`).
- **Scheduled work:** twelve pg_cron jobs active at the 2026-08-20 readback, including the nightly `retention-cleanup` added that day (release state, "Scheduled work actually running").
- **Pricing:** Free, and Edge Pro at $49 monthly. Canonical in `supabase/functions/_shared/edge-pricing.ts`; `public/.well-known/product.json` mirrors it and `npm run docs:check` fails if they disagree.
- **Compliance:** controls in place are listed at `/trust` and in `project-documentation/compliance/`; no SOC 2 report, no ISO 27001 certificate, HIPAA out of scope.
- **Documentation:** 64 files uploaded on 2026-09-04 without headers were classed Historical and moved to `docs/history/` on 2026-09-07; nine reconciled docs the upload overwrote were restored (`docs/history/LOG.md`). The release receipt in `docs/current/release-state.md` still describes `860dea0`, and later `main` commits are code and documentation changes that receipt does not cover.
- **Built but not live:** the gather-keeping tables from 2026-09-22 (migration not applied per the merge message). **Waiting on evidence, not code:** deployment of `video-radar-export`, the PR #375 change and the PR #398 privacy change.

## What changed recently

- 2026-10-18 **Every session now starts from the North Star** (`e10fea26`, `596a088b`). Why: Krish ruled that every repository has one and every session anchors to it. Ruling (Krish, 2026-10-18): "North Star timeframes assume agents do the work, not humans." The horizon is 100 leaders turning the flywheel every week by March 2027 (`project-documentation/NORTH_STAR.md`).
- 2026-10-17 **Repository operating context administered** (PR #399). Why: the approved rollout generates `docs/HARNESS_CONTEXT.md` and a hash and budget check workflow from the central record, and it matched the generated candidate exactly before merging. Those files belong to that publisher, not to the steward.
- 2026-10-15 **OpenAI Chat Completions no longer store requests** (PR #398). Why: the shared client never sent `store: false`, so `callOpenAI` and `streamOpenAI` in `supabase/functions/_shared/openai-utils.ts` used the provider default. The same change binds the privacy functions to the configured project through the new `project-binding.ts` and restores the `measure-standard` source. No deployment readback is recorded here.
- 2026-10-15 **The docs steward moved to `krishanraja/ai-harness`** (PR #397). Why: control-center went private and a public repository cannot call a private repository's reusable workflow.
- 2026-09-22 **The gather is kept, not only the feed** (`a6ce832a`, merged in `83ce7c48`). Why, in the commit's words: "live-headlines fetches several hundred AI stories a day and serves twenty... the rejected majority never existed as data." Three append-only tables record every article with its verdict, every version of a cached day, and the daily model leaderboard; the shared pool going dark for four weeks to 2026-08-05 went unreported. `cleanup-expired-data` had deleted nothing since it was written because it targeted a table no migration creates. The merge message says migration `20260922100000_ctrl_keeps_what_it_gathered.sql` was NOT APPLIED to any database, so the code is merged and inert. No later readback is recorded.

## What is next and what is waiting on Krish

- Next engineering gate: one designated synthetic Brain workspace, the server-side encrypted write adapter built on the existing primitives, the committed multi-identity database suite on a writable non-customer connection, and a read-only projection before any approved Brain UI consumes real substrate data.
- Waiting on Krish: a deployment readback for `video-radar-export`, the PR #375 change and the PR #398 change, then a line in `docs/current/release-state.md`.
- Waiting on Krish: whether to apply `20260922100000_ctrl_keeps_what_it_gathered.sql` to the shared project. The commit calls it a decision for a person, and the `cleanup-expired-data` delete stays off behind `CLEANUP_PRUNE_AI_CACHE`.
- Waiting on Krish: the repository is now named `mindmake-ctrl` on GitHub while `fleet.json` still lists it as `mm-ctrl`.
- Waiting on Krish: the product name. The fleet calls this "CTRL by Mindmake"; the repo's README title, `product.json` (`legal_entity`, `parent` link) and compliance pack say "Mindmaker". The steward does not change names or commercial claims.
- Waiting on Krish: whether the corpus and course material archived today (the `doc-*`, syllabus and `DECISIONING CORPUS` files) belongs in another repository, and whether `docs/CTRL-BRAIN-ARCHITECTURE.md` (now in history) should be re-headed as a Reference for the brain migrations that cite it.
- Waiting on Krish: three uploaded files outside the steward allowlist, `docs/_INTERROGATION_RESULTS.json`, `docs/check-standards.mjs` and `docs/ctrl-wordmark.png`.

## Read next

1. `docs/current/README.md`: the index and the authority order. Every current and reference document is listed there.
2. `docs/current/release-state.md`: the exact production baseline, what is deployed, what is only merged, and the live cron schedule.
3. `docs/current/commercial.md` and `public/.well-known/product.json`: buyer, offer, proof, claims and their machine-readable twin. The only sources for a price or a claim.
4. `docs/current/product.md` and `docs/current/features.md`: the user, the promise, the experience laws, and every live route.
5. `docs/current/architecture.md`: boundaries, data flows, the shared Supabase project, provider routing.
6. `project-documentation/DECISIONS_LOG.md`: accepted decisions with unique IDs. Decision 82 is the personal frame.
7. `CHANGELOG.md`: how it got here, newest first.
8. `CLAUDE.md` and `docs/agent-instructions/`: rules for coding agents in this repo.

## Do not trust

- Anything under `docs/history/2026-09-07-*` (64 files): the 2026-09-04 upload, classed Historical today. Surface maps (`app-*`), intelligence distillations (`intel-*`, `_INTELLIGENCE-LAYER`), Phase 0 specs and Phase 1 dead-code manifests describe the June 2026 app on the retired `ctrl.themindmaker.ai` host and are replaced by `docs/current/`. `GTM-PLAN` and `doc-icp` carry retired positioning and prices; `docs/current/commercial.md` wins. `CTRL-BUILD-ROADMAP` and `CTRL-CORPUS` were unlabelled copies of the Historical files in `project-documentation/`. `LLM_CRITICAL_THINKING_TRAINING` duplicates the manual that ships with `ai-generate`. The six `md*.md` files were untitled research dumps. The banner on each names its replacement.
- The revisions of `docs/AGENTIC_UI_TESTING.md`, `BRIEFING_GENERATION_HISTORY.md`, `CTRL-SYSTEM-SPEC.md`, `CURATION-SYSTEM-SPEC.md`, `ENRICHMENT-CONVERGENCE.md`, `HARNESS-CHAIN-STATE.md`, `KIT-REDESIGN-SPEC.md`, `MAIN-APP-POLISH-SPEC.md` and `PORTFOLIO-HIVE-MIND.md` at commit `8174677`: headers stripped, overlay restored. The 2026-08-20 revisions are back in place since 2026-09-07.
- `docs/current/architecture.md` before 2026-09-07: it said `backfill-pseudonymise` was undeployed and counted 177 functions; both were superseded by the 2026-08-21 release. `CHANGELOG.md` before 2026-09-07 had no entry for PRs #371 and #375.
- The test-account table in `docs/AGENTIC_UI_TESTING.md`: `example.com` placeholders, not accounts.
- `project-documentation/CTRL-BUILD-ROADMAP.md`, `CTRL-CORPUS.md`, `HISTORY.md`, `APP-DELIVERY-STATE.md` and the commercial files listed as historical in `docs/current/README.md`: labelled Historical and left in place by Krish's 2026-08-20 reconciliation.
- The `2026-09-22` entry in `CHANGELOG.md` opens with "Not merged, not applied to production". The code merged in `83ce7c48`; the migration still has no apply record. Read it with that correction.
- `docs/current/release-state.md` and `docs/current/architecture.md` carry `Last verified: 2026-09-08` and describe the G16 release. They were not re-verified against deployment after that date.
- Any document naming `ctrl.themindmaker.ai` as the host: retired, a permanent redirect only.
