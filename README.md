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

## RecallLint — lint your agent's memory before it lies to your agent

**[RecallLint](https://github.com/Yalakala-Naveen/recalllint)** (v0.1.0) — coding agents now keep persistent memory files (`CLAUDE.md`, `AGENTS.md`, `MEMORY.md`) and treat them as ground truth, but nothing checks them: a memory learned three weeks ago can be confidently wrong after a refactor, and every agent sharing it inherits the mistake. RecallLint audits those files against the repo as it is today — dead paths, dead symbols, stale sources (per git history), unsourced claims, duplicates — with a report, `--json` output, and CI exit codes. Deterministic; no model in the verdict path. Built from the loudest stated gap in Product Hunt's agent-memory launch threads. 35/35 tests. Launched on Product Hunt Nov 20, 2026. PyPI release pending (install from the GitHub release today).

- **Try it in your browser:** [RecallLint Playground](https://yalakala-naveen.github.io/recalllint/) — paste a memory file and your repo's file list, get the report. Nothing uploaded.
- **Product Hunt:** [RecallLint on Product Hunt](https://www.producthunt.com/products/recalllint?launch=recalllint)
- **Code:** https://github.com/Yalakala-Naveen/recalllint

## ScrubZero — v2 in build (PyPI launch held)

**[ScrubZero](https://github.com/Yalakala-Naveen/scrubzero)** — zero-dependency PII and secret redaction for logs, prompts and datasets. Checksum-validated before anything is masked (Luhn for cards, mod-97 for IBANs), so a 16-digit order id survives and a real card doesn't. The lightweight redaction seat has been empty since scrubadub's last push in Sep 2023, against ≈8.8M downloads/month of counted demand (Presidio + scrubadub, pypistats Nov 2026). 32 tests passing; PyPI launch held under the Buyer-First model — v2 adds credential redaction (passwords, tokens, database URLs) before any publish.

- **Playground:** https://yalakala-naveen.github.io/scrubzero/
- **Code:** https://github.com/Yalakala-Naveen/scrubzero

## RxGuard — fraud detection with no labels

**[RxGuard](https://github.com/Yalakala-Naveen/rxguard)** — prescription fraud has no labels to train on, so RxGuard detects pill mills, doctor-shopping rings, and forged-prescription bursts unsupervised: an Isolation Forest + PCA detector over prescriber behaviour, plus a graph detector (doctor-shopping windows, shared-patient clusters) over the prescriber–patient–pharmacy network, on a synthetic dataset modeled on public CMS Part D patterns. The detectors never see the injected ground truth; scored against it, the combined ranking reaches recall@20 1.00 with all 12 doctor-shoppers found — and the weak spot is printed in the README too: feature-only precision@10 is 0.30. 16/16 tests.

- **Live demo (UI twin):** https://yalakala-naveen.github.io/rxguard/ — click any flagged prescriber and see exactly why it was flagged
- **Code:** https://github.com/Yalakala-Naveen/rxguard

## More

- **Portfolio:** https://yalakala-naveen.github.io
- **LinkedIn:** https://www.linkedin.com/in/naveen-y-b47090122
