# Prompt Composer

A structured prompt-engineering tool built around the **R-G-C-B-T-S** frame.

**Live:** <https://prompt.phbeks.com> · **Repo:** <https://github.com/deokman420/prompt-composer>

Built so anyone trying to write a better prompt has a place to *think* in the right slots — and a way to learn the structure by seeing it everywhere on the page.

## What it does

1. **Six core slots — R-G-C-B-T-S** — Role, Goal, Context, Bounds, Task, Success. Each with a one-line hint and clickable suggestion chips (specific, research-backed — e.g., "Senior data analyst" not "expert").
2. **Examples slot** — up to 3 input/output pairs. Few-shot is the single highest-impact technique per Anthropic's published research; making it a first-class slot reflects that.
3. **Live preview, Markdown ↔ XML** — see the composed prompt update on every keystroke; toggle output between markdown headings and XML tags (XML is the Claude-preferred shape for mixed-content prompts).
4. **Composition score** — local, structural rubric (0–100). Honest about what it measures: completeness and structure, not quality. Tracks personal best + lifetime count.
5. **Starter templates** — 8 complete pro-prompts (Code reviewer, Bug repro, Meeting actions, Doc rewriter, ADR, Email triage, Test plan, Tutorial writer).
6. **Prompt Archaeology** — 6 famous prompts decomposed into the R-G-C-B-T-S frame: Claude system prompt, v0 by Vercel, Cursor IDE, GitHub Copilot, ReAct (Yao 2022), Chain-of-Thought (Wei 2022). Reverse-engineering practice — see how the pros structure intent.
7. **Shareable URLs** — encode the full form state as a base64 fragment. The fragment never reaches a server; anyone you send it to opens the link and the form auto-populates.

## How it works

- **Single-page static site.** No backend, no API calls, no analytics, no tracking.
- **Persistence is localStorage only** — current draft, saved drafts, theme, format, personal best, lifetime count.
- **Share links** use the URL hash (`#s=…`), which browsers never transmit to servers.
- Drop the whole folder onto any static host (Vercel, Netlify, GitHub Pages, S3, an nginx box) and it works.

## How to use

### Online

Visit **<https://prompt.phbeks.com>**. Works in any modern browser. Mobile-friendly (iOS Safari, Android Chrome).

### Console easter egg

Open DevTools. The console has lore. Type `rgcbts` anywhere on the page for the keyboard egg.

### Offline

Clone the repo and open `index.html` directly — no build, no dev server needed.

```sh
git clone https://github.com/deokman420/prompt-composer
cd prompt-composer
# open index.html in your browser
```

## The R-G-C-B-T-S frame

| Slot | What it controls |
|------|------------------|
| **Role** | Who the model acts as (1 line) |
| **Goal** | Single outcome, verb-first |
| **Context** | Load-bearing facts the model can't infer |
| **Bounds** | Out of scope / forbidden |
| **Task** | Concrete steps or deliverable shape |
| **Success** | Checkable "done" criteria |
| _Tools_ | Allowed / forbidden tools or sources (optional) |
| _Format_ | Output shape: JSON keys, length cap, headings (optional) |
| _Clarify_ | "Ask N questions first if X is ambiguous" (optional) |

## Composition score (honest disclaimer)

The score measures **structural completeness**, not **prompt quality**. It cannot tell whether your prompt will produce a good response — only whether it has the structural ingredients we know correlate with good results. Don't write to game the score.

| Signal | Pts | Triggers when |
|--------|-----|---------------|
| Slot completeness | 30 | 5 per filled core slot |
| Role specificity | 10 | ≥40 chars + a specifier ("senior", "with N years", domain noun) |
| Goal verb-first | 10 | First word is an imperative verb |
| Bounds non-trivial | 10 | ≥20 chars + "don't"/"no"/bullet |
| Task specificity | 10 | ≥50 chars OR numbered list / multi-line |
| Success checkable | 10 | ≥30 chars + concrete output noun |
| Examples present | 10 | ≥1 complete input/output pair |
| Add-on adoption | 10 | Any of Tools/Format/Clarify |

Personal best only updates on scores ≥ 60 so early experiments don't pollute it. Lifetime count increments on copy actions (the "I actually used it" signal).

## Deployment

This repo deploys to Vercel automatically on every push to `main` via the workflow in `.github/workflows/deploy.yml`. Requires three repo secrets: `VERCEL_TOKEN`, `VERCEL_ORG_ID`, `VERCEL_PROJECT_ID`.

To deploy your own copy elsewhere: clone the repo, drop the four files (`index.html`, `app.js`, `style.css`, `favicon.svg`) onto any static host.

## License

MIT — see [`LICENSE`](LICENSE).
