---
repo: krishanraja/mm-ctrl
product: CTRL by Mindmake
as_of: 2026-10-15
head: 9cc46ab
head_scope: OpenAI chat storage disabled and project-bound privacy functions
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

## Where it is right now (as of 2026-10-15)

- **Live** at `makeyourmindup.ai`. The last recorded production receipt is the G16 application release `860dea0`, Vercel `dpl_2JFRfmZRzUvxbdwXqLunG3eubTgc`, READY and PROMOTED from that SHA (`docs/current/release-state.md`). `main` has moved on since: Vercel builds every push, but no deployment receipt is recorded here for the newer commits.
- **Merged to `main`, no deployment readback recorded:** the OpenAI `store: false` change and the `measure-standard` function source (PR #398, `9cc46ab`), the strict Brain adapter primitives and the synthetic population lab (PRs #385, #388, #389, #391, #392, all dormant or preview-gated), and the gather-record code in `live-headlines` (`a6ce832`).
- **Committed but not applied:** the migration `supabase/migrations/20260922100000_ctrl_keeps_what_it_gathered.sql`. `CHANGELOG.md` says no migration has been run against the shared project. Treat the new record tables as not existing in production until a readback says otherwise.
- **Edge Functions:** 116 directories in the tree and 171 migration files (`docs/current/release-state.md`, measured 2026-10-15). 183 live on the shared project at the 2026-09-05 readback; that is deployment inventory, not repository ownership. `measure-standard` is new in the tree with no deployment readback.
- **Tests:** 945 tests in 60 files with zero new type errors against the 94-error legacy baseline, recorded at the G16 release `860dea0`. Not re-measured since.
- **Living Brain substrate:** 11 additive production tables are live, empty and disconnected from customer paths. The G17 adapter modules (`_shared/brain-crypto.ts`, `_shared/brain-ingest-core.ts`) have tests but no runtime calls them. The G18 synthetic lab is an unlinked, `noindex`, preview-gated route. The G20 capture and Claude bridge exists as a contract only (`project-documentation/ctrl-evolution/README.md`).
- **Scheduled work:** twelve pg_cron jobs active at the 2026-08-20 readback (release state, "Scheduled work actually running").
- **Pricing:** Free, and Edge Pro at $49 monthly. Canonical in `supabase/functions/_shared/edge-pricing.ts`; `public/.well-known/product.json` mirrors it and `npm run docs:check` fails if they disagree.
- **Compliance:** controls in place are listed at `/trust` and in `project-documentation/compliance/`; no SOC 2 report, no ISO 27001 certificate, HIPAA out of scope.
- **Waiting on evidence, not code:** deployment readbacks for `video-radar-export`, the PR #375 change, `measure-standard` and the PR #398 edits; application of the 2026-09-22 migration.

## What changed recently

- 2026-10-15 **OpenAI chat storage switched off, and the project check made exact** (PR #398, `9cc46ab`). Both Chat Completions calls in `_shared/openai-utils.ts` now send `store: false`, so the provider does not retain the prompts. In the same change `build-sort`, `compile-standard` and `critique-artefact` stopped checking that the Supabase URL merely contained a hard-coded project id and now compare the host exactly with `<ref>.supabase.co`, the ref read from `EXPECTED_SUPABASE_PROJECT_REF` (`_shared/project-binding.ts`). A substring test passes for any URL that includes the id. The commit also restores the `measure-standard` source. No deployment readback.
- 2026-10-15 **The docs steward now runs from `krishanraja/ai-harness`.** Why, in the commit's words: "control-center goes private on 2026-10-15, and a public repository cannot call a reusable workflow in a private one." The workflow, runbook, schema, fleet manifest and scripts moved unchanged (`b767394d`).
- 2026-09-22 **The gather is kept, not only the feed** (`a6ce832`). Why: `live-headlines` fetches several hundred AI stories a day and serves twenty, and "the rejected majority never existed as data", so volume, share of voice and any audit of the filters were unanswerable. Three append-only record tables, enforced by trigger, keep every article with its verdict and an absolute `published_at`, every version of a cached day, and the daily Artificial Analysis board. A runs table records per-source counts because "the shared pool went dark for four weeks to 2026-08-05 and nothing reported it." The same change found `cleanup-expired-data` had deleted nothing since it was written, because it targeted `ai_cache`, a table no migration creates. The real delete stays off behind `CLEANUP_PRUNE_AI_CACHE`: "a delete that has never run ... is a person's decision rather than a side effect of a one-word fix." The feed is unchanged. Migration committed, not applied (`CHANGELOG.md`).

## What is next and what is waiting on Krish

- Next engineering gate (`project-documentation/ctrl-evolution/README.md`, NEXT_ACTION): publish and run the fixed G17 branch-creation workflow once the GitHub session has separately approved `workflow` scope, apply the G16 migrations on the isolated branch and run the committed behavioural suite before seeding the G18 population. No real customer data and no public Brain surface without a separate founder gate.
- Waiting on Krish: deployment readbacks for `video-radar-export`, the PR #375 change, `measure-standard` and PR #398, then a line in `docs/current/release-state.md`. The three project-bound functions need `EXPECTED_SUPABASE_PROJECT_REF` set when deployed, or the check returns false for an empty ref (`_shared/project-binding.ts`).
- Waiting on Krish: whether to apply the 2026-09-22 migration to the shared project, and whether to ever turn on `CLEANUP_PRUNE_AI_CACHE`.
- Waiting on Krish: the product name. The fleet calls this "CTRL by Mindmake"; the repo's README title, `product.json` (`legal_entity`, `parent` link) and compliance pack say "Mindmaker". The steward does not change names or commercial claims.
- Waiting on Krish: whether the corpus and course material archived on 2026-09-07 belongs in another repository, and whether `docs/CTRL-BRAIN-ARCHITECTURE.md` (now in history) should be re-headed as a Reference for the brain migrations that cite it.
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
- Any document naming `ctrl.themindmaker.ai` as the host: retired, a permanent redirect only.
