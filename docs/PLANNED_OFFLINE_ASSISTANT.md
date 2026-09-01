# Planned Follow-Up — Offline Docs + Local LLM Assistant

Captured so it isn't lost. **Not started.** Sequenced AFTER: (1) finishing Android setup on all
three phones, (2) profile tuning, (3) the Field Manual docs. The Field Manual is a prerequisite —
it becomes the assistant's source material.

## Part 1 — Offline complete docs ("Field Manual")

Goal: full, offline, self-contained docs for the whole diabetes stack — how each app works,
settings, integration, FAQ, troubleshooting — usable with no internet.

Two layers, kept honestly separated:
- **Layer 1 — mirrored authoritative sources, unedited.** Official AAPS (readthedocs), xDrip+
  wiki, Omnipod/Dexcom guides, downloaded as PDF/HTML. The clinical ground truth; not rewritten.
- **Layer 2 — the Field Manual (written for THIS setup).** Connective tissue the official docs
  lack: how the *eternal* build differs from stock, the exact chain (G7 → BYODA/xDrip → AAPS →
  DASH), real problems hit during setup, break-glass steps. Clinical specifics point back to
  Layer 1 rather than restating them.

Format: one self-contained **offline HTML file** (inline styling/diagrams, opens in any phone
browser, searchable) + the official PDFs alongside. Stored on each phone + USB in kit + repo.

Proposed sections: system map · how it works · per-app reference (AAPS incl. eternal changes,
xDrip+, BYODA, Dexcom G7, Omnipod DASH, Eros+RileyLink, Medtronic) · integration & data flow ·
setup procedures · break-glass · FAQ · troubleshooting (incl. signature-mismatch on update,
Gradle/AGP/JDK build errors, "NO PROFILE SET" with no pod, folder/import) · cold storage &
maintenance · Layer 0 MDI emergency card · glossary.

Open decisions: Trio in or out (iPhone being retired); Medtronic depth (needs model/firmware
numbers); fetch official PDFs now vs link them; keep actual dosing values OUT of the (public)
repo — use fill-in tables.

Banner on every page: **reference only; never overrides clinical judgment or the care team.**

## Part 2 — Local (offline) LLM to query the docs

Goal: a language model running entirely on the owner's hardware, pointed at the Field Manual +
the owner's own survival doc, answering questions with no internet. This is **local RAG**
(retrieval-augmented generation).

**Safety rule (non-negotiable):** the LLM is a search-and-explain convenience layer, NEVER a
dosing authority. Run in **citation/RAG mode** so it quotes the source doc; always verify against
the actual doc. The printed/HTML docs remain ground truth. For pure grid-down reliability,
well-indexed docs + text search beat an LLM (no hallucination, negligible power) — the LLM sits
on top as convenience.

Design choices to make:
- **Host:** phone-in-the-bag (most doomsday-aligned, small 1–4B models via PocketPal / ChatterUI /
  MLC Chat / Layla) · dedicated low-power Raspberry Pi/mini-PC (solar-friendly oracle) · or the
  Mac at home (best answers, 7–14B, but needs power).
- **Software (beginner-friendly, offline):** GPT4All **LocalDocs**, or AnythingLLM, or LM Studio
  "chat with documents"; power-user: Ollama + Open WebUI.
- **Models (quantized GGUF):** Llama 3.2 3B, Qwen 2.5 3B/7B, Phi-3.5, Gemma 2 2B/9B. RAG does the
  heavy lifting, so even a 3B model is useful and phone-friendly.
- **Purpose:** daily convenience vs strictly break-glass (break-glass favors phone/Pi).
- **Survival doc format:** (owner's separate doc) — PDF/Word/Markdown/plain text all RAG-index
  fine; determines ingestion path.

Recommended first step: stand up **GPT4All on the Mac**, point LocalDocs at the repo docs + the
survival doc as a ~20-minute proof of concept, evaluate answer quality, THEN decide whether to
deploy a small model + RAG on a phone or Pi for the kit.
