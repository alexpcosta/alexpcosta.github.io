# Session Improvement Report — alexpcosta.github.io

**Date:** 2026-07-12
**Prepared by:** Claude (Claude Code remote session)

> Note: this file lives in a **public** repository. If you'd rather keep it private,
> don't merge this branch — read it here and delete it, or move it to a private repo.

---

## 1. What this analysis is based on (and what it isn't)

Remote sessions run in ephemeral containers, so transcripts of previous conversations
are not available here. This is an **artifact-based** review: git history, branches,
pull requests, GitHub Actions runs, the live-site configuration, and the session
environment itself. Sessions you've run against your other repositories
(StratOS, salta-muros-wc26, Modern-Family-v2, DevPipeline, etc.) are outside this
session's repository scope, so this report covers the `alexpcosta.github.io` work
plus general workflow patterns visible from here.

**Activity timeline for this repo:**

| Date | Event | Author |
|------|-------|--------|
| 2026-03-27 | Repo created: README (F&F Brain Duel PRD), `privacy-policy.md`, `app-ads.txt` | Alex (direct commits) |
| 2026-05-31 | Claude session "game-from-image" → PR #1: Domineering game (463-line single file) | Claude session |
| 2026-07-12 | This session (improvement analysis) | Claude session |

---

## 2. Headline finding: work gets built, then stalls at the finish line

**PR #1 ("Add Domineering game implementation") has been open and mergeable for 6 weeks.**
It has a clean mergeable state, zero review comments, zero CI failures — nothing is
blocking it. The game was fully built on 2026-05-31 and has delivered zero value since,
because GitHub Pages deploys from `main` and the code never got there.

Even if merged today, the game would still be invisible: the site has **no index page
linking to `/domineering/`**, so nobody would find it without knowing the URL.

This is the single clearest pattern to fix, and it has a "you" half and a "me" half:

- **You:** treat "merged and reachable" as the definition of done, not "PR opened."
  Merge or close PR #1 this week.
- **Claude:** the session that opened the PR should have (a) pointed out that merge =
  deploy on this repo, (b) offered to watch the PR (`subscribe_pr_activity`) or enable
  auto-merge, and (c) flagged that nothing links to the new page. Fire-and-forget PRs
  against a personal site with no reviewers just become stale.

---

## 3. Findings about the site itself

These surfaced while auditing, and each one is a small task Claude can do on request:

1. **Your public homepage is a draft PRD.** GitHub Pages uses `README.md` as the site
   entry file when there's no `index.html`/`index.md`, so `https://alexpcosta.github.io/`
   renders the full F&F Brain Duel product requirements document (marked "Status: Draft"),
   including unreleased features. If that's not intentional, add a proper `index.html`
   landing page (links to your games, apps, privacy policy) and move the PRD into a
   private repo or Confluence (your Atlassian connector is already hooked up).

2. **Two privacy policies, two URLs, drift risk.** The README links to
   `https://alexpcosta.github.io/F-F-Brain-Duel/privacy-policy` (served from the
   separate `F-F-Brain-Duel` repo), while a second copy lives in this repo as
   `privacy-policy.md`. Also, `privacy-policy.md` has no Jekyll front matter, so the
   extensionless URL `/privacy-policy` on this site almost certainly 404s (the file is
   served raw at `/privacy-policy.md`). Pick **one canonical URL** — the one registered
   in App Store Connect / Play Console — delete or redirect the other, and verify it in
   a browser. I could not verify the live URLs from this environment (see §5).

3. **`app-ads.txt` placement looks correct** (root of the user site, required by AdMob).
   Worth a one-time check that the developer URL in your app store listings actually
   points at `alexpcosta.github.io`, since app-ads.txt only works when it matches.

4. **Repo sprawl around Brain Duel.** Your account has `F-F-Brain-Duel`,
   `FF-Brain-Duel-iOS`, `brain-duel-android`, and `BrainDuelApp`. Any session (or human)
   touching this project has to guess which is canonical. A one-line note in each README
   ("superseded by X" / "canonical iOS repo") would prevent wasted sessions.

---

## 4. What you can do better

1. **State the definition of done in the first prompt.** "Build the game from this
   image" produced good code; "Build it, link it from the homepage, merge it, and
   confirm it's live" would have produced a shipped game. When a PR is the output, say
   whether you want it merged, watched, or left for review.

2. **Close the loop on PRs.** You're the only reviewer in this repo. An open PR with no
   reviewer is a parking lot. Either ask Claude to merge once checks pass
   (auto-merge is available via the GitHub tools), or ask it to babysit the PR —
   remote sessions can subscribe to PR events and react to comments/CI without polling.

3. **Add a `CLAUDE.md` to each active repo** (the `/init` skill does this). Right now
   every session rediscovers from scratch that this repo is simultaneously (a) a GitHub
   Pages user site, (b) the privacy-policy/ads host for your apps, and (c) a place for
   game experiments. Five lines about deployment ("Pages serves `main`, README is the
   homepage") would have changed what past sessions did.

4. **Fix the environment's network policy.** This environment's proxy denies outbound
   requests even to `alexpcosta.github.io` (CONNECT 403, policy denial). That means no
   session in this environment can verify the deployed site, check for 404s, or
   screenshot a live page. Allowlist your own domain (and anything else you want
   verified) in the environment's network settings on claude.ai/code — it converts
   "I think this deployed" into "here's a screenshot of it live."

5. **Ask for verification evidence.** Chromium + Playwright are pre-installed in these
   containers. For anything visual (games especially), ask for a screenshot in the PR —
   it costs the session a minute and gives you a review you can do from your phone.

---

## 5. What Claude can do better

Honest self-review of the visible session output:

1. **Verify, don't just build.** PR #1 shipped 463 lines of UI code with no screenshot
   and no evidence it was ever rendered, despite a bundled browser. Every future visual
   change should include a screenshot or a note that rendering was verified locally.

2. **Surface deployment consequences unprompted.** On this repo, "opened a PR" means
   "nothing is live yet" and "no index links to it" means "nobody can find it." Those
   two facts belonged in the PR description or the session's final summary.

3. **Offer follow-through mechanisms.** Sessions can subscribe to PR activity, enable
   auto-merge, or schedule a check-in (e.g., "in a week, remind me this PR is still
   open"). None was offered. Default going forward: when a session ends with an open PR,
   propose one of these.

4. **Flag adjacent problems.** The PRD-as-homepage and the privacy-policy URL mismatch
   were visible to any session that opened the README. Staying narrowly on-task is right
   for the code, but a one-line "heads-up, your homepage is a draft PRD" belongs in the
   summary.

(For balance: the Domineering implementation itself is clean — correct rules including
the loss-on-no-move condition, undo that restores turn order properly, mobile-friendly,
zero dependencies. The gap was delivery, not code quality.)

---

## 6. Tools worth adopting

Already available in your sessions, mostly unused so far:

| Tool / feature | What it buys you | How to use |
|---|---|---|
| **PR activity subscription** | Session watches a PR, fixes CI failures, responds to comments | "watch this PR and autofix CI" |
| **Auto-merge** | PRs land the moment checks pass, no parking lot | "enable auto-merge on this PR" |
| **Routines / scheduled triggers** | e.g. weekly repo-hygiene check: stale PRs, broken links, drift between privacy-policy copies | "set up a weekly routine that…" |
| **`/init` skill** | Generates `CLAUDE.md` so sessions start with context | Run once per active repo |
| **`/verify` and `/code-review` skills** | End-to-end verification and a bug-focused review pass before a PR goes up | Ask for them before "open a PR" |
| **Playwright + Chromium (pre-installed)** | Screenshots of pages/games as PR evidence | "include a screenshot in the PR" |
| **Artifacts** | Private preview page of a game/UI before anything is committed | "show me a preview first" |
| **Atlassian connector (already connected)** | Move the PRD to Confluence; track app backlog in Jira instead of a README | "create a Confluence page from this README" |
| **Link-check CI** (suggestion) | A tiny GitHub Action (e.g. lychee) that fails on broken links — would have caught the privacy-policy 404 risk | Ask a session to add it |

---

## 7. Suggested next actions (in order)

1. Merge or close **PR #1** — it's clean and waiting.
2. Ask a session to build a real **`index.html` homepage** (links to Domineering, your
   apps, privacy policy) and demote the PRD from homepage duty.
3. Decide the **canonical privacy-policy URL**, fix the README link, remove the
   duplicate, and verify the URL in a browser (this is app-store-facing).
4. Run **`/init`** here (and in StratOS + whatever else is active) to create `CLAUDE.md`.
5. **Allowlist `alexpcosta.github.io`** in this environment's network policy so future
   sessions can verify deployments.
6. Optionally: a weekly **routine** that checks this repo for stale PRs and broken links.

Each of items 1–4 is a five-minute ask in a future session — or all four in one.
