# Naveen Yalakala

**Forward Deployed Engineer — I make agents survive production.**

Forward Deployed Engineer at ADP. Architect of ADP's production AI Search and AI Assist platforms: hybrid retrieval that improved search precision by 35%, LangGraph multi-agent routing across Payroll, Tax, Benefits and HR, held to 99.9% uptime by evaluation and monitoring pipelines.

I build the verification layer production AI is missing — the checks that catch an agent claiming "done" when the work isn't.

## FailLoud — the done-check for AI agent output

**[FailLoud](https://github.com/Yalakala-Naveen/failloud)** (v0.6.0) — a deterministic verification harness for LLM agent outputs. Agents rarely fail loudly: they return `status: "done"` with placeholder content, claims with no evidence behind them, counts their own records contradict. Every dashboard stays green because the agent graded its own homework. FailLoud reads the output the way a skeptical reviewer would. No model in the verdict path — every verdict is deterministic and explainable line by line.

Six checks:

| Check | Catches |
|---|---|
| FL001 `placeholder_shipped` | Output declared done while the payload is empty or still holds draft scaffolding |
| FL002 `unbacked_claim` | A claimed action (sent, posted, published…) with no id, URL, receipt, or artifact behind it |
| FL003 `stale_state` | Work based on state older than allowed, or a state-version skew between handover and run |
| FL004 `count_mismatch` | A reported count that disagrees with the itemized record in the same document |
| FL005 `missing_components` | Required fields present-but-empty, and dead stretches inside segmented deliverables |
| FL006 `unsupported_answer` | A RAG answer whose citations resolve to nothing retrieved, whose cited sources are empty, or whose numbers appear in no source |

Also in the box: hash-chained verification receipts (a verdict you can prove, not just quote), watch mode, second-pass verification against the system of record (every PASS is provisional until the record confirms it), a LangChain adapter, an MCP server, and a GitHub Action for CI.

- **Install:** `pip install failloud` — [PyPI](https://pypi.org/project/failloud/)
- **Try it in your browser:** [FailLoud Playground](https://yalakala-naveen.github.io/failloud/) — paste an agent output, get the failure report. No install, nothing uploaded.
- **MCP Registry:** listed as `io.github.Yalakala-Naveen/failloud` in the [official MCP Registry](https://registry.modelcontextprotocol.io)
- **Code:** https://github.com/Yalakala-Naveen/failloud

## tidyexcel — messy spreadsheet in, tidy DataFrame out

 **[tidyexcel](https://github.com/Yalakala-Naveen/tidysheet)** — real-world Excel/CSV exports arrive with title rows, merged multi-row headers, totals and footnote rows baked into the data, and pandas detects none of it: everyone hand-rolls the same `skiprows=`/`ffill` glue per file. tidyexcel detects the structure — title rows, merged headers, totals, footnotes, merged data cells — and returns a clean DataFrame plus a report listing every fix. Deterministic heuristics, no AI in the path.

- **Live demo (runs in your browser, nothing uploads):** https://yalakala-naveen.github.io/tidysheet/
- **Code:** https://github.com/Yalakala-Naveen/tidysheet
- **Install:** `pip install tidyexcel`

## PulseProof — proof of a live human for AI agent approvals

**[PulseProof](https://github.com/Yalakala-Naveen/pulseproof)** — an AI agent about to do something irreversible should have to prove a live human is present, not just that a password was typed once. PulseProof issues a fresh random breathing-pacer challenge (~12s, with a mid-stream rhythm change) read through the Presage SmartSpectra SDK — live pulse plus breathing tracking plus rhythm consistency against an enrolled baseline — and issues a hash-chained presence receipt on PASS. Honest limits, stated in the repo: liveness and consistency, never biometric identity. 24/24 tests; the synthetic attack matrix is published in the README (flat signals 0/60 pass, constant-rate 0/60, honest trackers 120/120). DEV Presage SmartSpectra SDK Challenge entry — submission deadline Nov 22, 2026; live-camera test runs Nov 18–19.

- **Code:** https://github.com/Yalakala-Naveen/pulseproof

## ScrubZero — coming Mon Nov 23, 2026

**[ScrubZero](https://github.com/Yalakala-Naveen/scrubzero)** — zero-dependency PII and secret redaction for logs, prompts and datasets. Checksum-validated before anything is masked (Luhn for cards, mod-97 for IBANs), so a 16-digit order id survives and a real card doesn't. The lightweight redaction seat has been empty since scrubadub's last push in Sep 2023, against ≈8.6M downloads/month of counted demand (Presidio + scrubadub, pypistats Nov 2026). 32 tests passing; PyPI publish Mon Nov 23.

- **Playground:** https://yalakala-naveen.github.io/scrubzero/
- **Code:** https://github.com/Yalakala-Naveen/scrubzero

## RxGuard — fraud detection with no labels

**[RxGuard](https://github.com/Yalakala-Naveen/rxguard)** — prescription fraud has no labels to train on, so RxGuard detects pill mills, doctor-shopping rings, and forged-prescription bursts unsupervised: an Isolation Forest + PCA detector over prescriber behaviour, plus a graph detector (doctor-shopping windows, shared-patient clusters) over the prescriber–patient–pharmacy network, on a synthetic dataset modeled on public CMS Part D patterns. The detectors never see the injected ground truth; scored against it, the combined ranking reaches recall@20 1.00 with all 12 doctor-shoppers found — and the weak spot is printed in the README too: feature-only precision@10 is 0.30. 16/16 tests.

- **Live demo (UI twin):** https://yalakala-naveen.github.io/rxguard/ — click any flagged prescriber and see exactly why it was flagged
- **Code:** https://github.com/Yalakala-Naveen/rxguard

## Klaviyo Bill Audit — free, in-browser

**[Klaviyo Bill Audit](https://github.com/Yalakala-Naveen/klaviyo-bill-audit)** — you're paying Klaviyo for people who will never buy again. Klaviyo bills on stored profiles; profiles that stopped opening, clicking, or buying 6+ months ago still count, and enough of them quietly push a store into the next price tier. This free audit counts a store's ghost profiles and what they cost every month. It runs 100% in the browser — the export is never uploaded anywhere.

- **Live tool:** https://yalakala-naveen.github.io/klaviyo-bill-audit/ (demo data: 7,130 ghosts of 12,400 profiles — $88/mo / $1,056/yr wasted)

## More

- **Portfolio:** https://yalakala-naveen.github.io
- **LinkedIn:** https://www.linkedin.com/in/naveen-y-b47090122
