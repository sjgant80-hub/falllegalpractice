# FallLegalPractice

**Sovereign single-file SRA Accounts Rules + practice accounting for UK solicitor firms.**

One HTML file. Runs in the browser. Data lives in your device's IndexedDB. Nothing leaves the device.

Part of the `falllegal` bundle (anchor 743 · onboard 751 · paper 757 · **practice 761**).

---

## For solicitors

If you run a 1-10 person SRA-regulated firm and you currently juggle spreadsheets for time, billing, the client account ledger, PII renewal, COLP/COFA duties, and CPD — this tool is for you.

What it does:
- **SRA Accounts Rules** ledger: separate client account and office account, rule 2.5 mixed-payment splits, rule 8.3 five-week reconciliation alarms, rule 7.1 interest watch
- **Time recording** in 6-minute units with CSV bulk import / export
- **Billing** built from accumulated WIP + disbursements + VAT, with client-account drawdown
- **Disbursements** (court / Land Registry / counsel / expert / search), VAT-aware
- **Per-adviser P&L** — WIP, billed, realisation rate
- **Firm P&L** — revenue, expenses, accruals, by practice area
- **PII tracking** — SRA £3M minimum, expiry alarms
- **COLP / COFA / AML supervisor** assignment, material breach register
- **CPD** progress (16hr SRA benchmark) per adviser
- **Audit chain** (Mansoor P3, prevHash on every write, 6yr SRA retention)
- **Q&A engine** for SRA rules (rule 2.5, 7.1, 8.3, VAT on disbursements, counsel fees, etc.)

What it does not do:
- Submit anything to the SRA on your behalf. Your COLP/COFA remain responsible.
- Replace your bank. The actual money lives at your bank — this tracks the ledger.
- Replace legal advice. It is a tool.

## Install

Open `index.html` in any modern browser. That's it. No server, no build, no account.

For an installed app feel: visit the GitHub Pages URL on your phone, "Add to Home Screen". PWA manifest is inline.

## Sync with the rest of the bundle

If `falllegal`, `falllegalonboard`, or `falllegalpaper` are open in another tab, this tool sync clients / advisers / matters automatically via `BroadcastChannel('fall-law')`. Send an invoice to FallLegalPaper for a polished PDF.

---

## For Claude / agents touching this repo

**Architecture:** one HTML file under 400KB. Vanilla JS, no frameworks, no build step, no CDN deps in core. IDB primary storage with localStorage settings fallback.

**Schema:** conforms to `LAW-BUNDLE-SHARED-SCHEMA.md` v1.0 — `Matter`, `LegalClient`, `LegalAdviser`, fall-law mesh, 6yr audit retention, SRA Accounts Rules data model.

**Constants:**
- `TOOLNAME = 'falllegalpractice'`
- `VERSION = '1.0.0'`
- `PRIME = 761`

**IDB stores (13):** state · clients · advisers · firms · matters · timeEntries · invoices · clientAccount · officeAccount · expenses · disbursements · piPolicies · audit

**Mesh messages (BroadcastChannel `fall-law`):** sync.request/snapshot · client.* · adviser.* · firm.updated · matter.* · clientAccount.entry · reconciliation.done · falllegalpaper.invoice.generate

**Estate cascade:** T0 SRA rules engine (14 rules) → T2 Ollama probe (127.0.0.1:11434) → T3 BYOK (Anthropic / Gemini / OpenAI / OpenRouter)

**Aesthetic:** oxblood `#8b1a1a` · brass `#b8974a` · cream `#e6e1d6` · void `#0b0a0f`. Georgia serif, Inter sans, IBM Plex Mono.

**Public API:** `window.FALLLEGALPRACTICE` exposes `recordTime`, `clientAccountHeld`, `ytd`, `wip`, `ask`, `interestWatch`, `unsplitMixed`.

**14-pt gate:** single HTML <400KB · IDB primary · KONOMI shim · two meshes · PWA manifest · mobile-first · MIT · two-audience README · `.nojekyll`. Conforms.

## License

MIT. See `LICENSE`.
