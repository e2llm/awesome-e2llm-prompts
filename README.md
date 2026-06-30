# E2LLM Prompt Recipes

> **Recipes for E2LLM — SiFR v3 capture format + the current MCP tool set.** If the SiFR format or the MCP tools change, these may need updating; check the version your install reports.

A practical cookbook for the **E2LLM** family — turning any web page into something an LLM can read, and any web UI into something an agent can operate.

## Why SiFR — not a screenshot, raw HTML, markdown, or the a11y tree
SiFR is a compact, LLM-readable representation of a page. It beats the alternatives for feeding a model because it is **compact** (a full page in a few hundred KB — fits a context window, where raw HTML is megabytes), **structure-preserving** (keeps the parent/child and sibling relations that markdown and a flat a11y tree drop), and **node-addressable** (every node has a stable id, so the model can point back at exactly the element it means — for references, selectors, or actions).

## Two surfaces, two jobs — pick the one you want

|  | **E2LLM** (browser extension) | **E2LLM MCP** (MCP server) |
|---|---|---|
| What it is | A browser extension that captures the page as **SiFR** | An **MCP server + bridge** that lets an MCP client drive the browser as tools |
| What it does | **Perception / capture** — "what is on this page", as text for an LLM | **Tool-use** — the model **perceives *and* acts**: query, read, click, type, navigate |
| You drive it by | Capturing SiFR (extension button, or the programmatic CustomEvent API) and pasting into your LLM | Connecting an MCP client (e.g. Claude Desktop); the model calls the tools itself |
| Best for | One-shot "give the model this page" — summarize, extract, compare, Q&A | Autonomous browser workflows — fill forms, follow links, multi-step tasks, QA/RPA |

**Rule of thumb:** if a *human* is copy-pasting page content into a chat, that is **E2LLM**. If the *model* is operating the web UI itself, that is **E2LLM MCP**.

## Capture presets (E2LLM)
A preset sets a **size ceiling** so the capture fits your model's context window — it is a *cap*, not a fixed size (a simple page captures well under it; the cap just guarantees you will not blow past it):
- **minimal** — smallest; structure only (drops styles, layout, low-salience nodes). Best for tight context windows.
- **visual** — adds computed styles + layout (positions and sizes).
- **normal** — the default; adds salience hints.
- **unlimited** — no ceiling; use only with large-context models when you genuinely need every node.

(The ceilings are byte budgets — minimal/visual/normal at 200/300/400KB, unlimited none. SiFR is compact text, so a byte budget is roughly proportional to tokens — treat the KB as a ballpark for context-fit, not an exact token count; it varies by tokenizer and page. Pick the smallest preset that captures what you need.)

## E2LLM (capture) recipes
Assuming you captured the page as SiFR and pasted it into your LLM.

**Summarize a dense page** — > Here is a SiFR capture. Give me a 5-bullet summary of the main content; ignore nav/footer/ads (use the SUMMARY and NODES sections).

**Extract structured data** — > From this SiFR capture, extract every product as JSON {name, price, rating}. Use NODES + RELATIONS to resolve which price/rating belongs to which product.

**Compare two versions** — > I am pasting two SiFR captures (BEFORE / AFTER). List exactly what changed in the main content — added, removed, edited. Ignore re-ordering of identical items.

**Answer strictly from the page** — > Using ONLY this SiFR capture, answer: <question>. If the page does not contain the answer, say "not on this page" — do not guess.

## E2LLM MCP (tool-use) recipes
Core tools: query (find elements), inspect (examine one), read_page (extract readable content), sifr_capture (capture SiFR), act (one action), batch_act (several in one pass), explore (drill into a section), list_tabs / close_tab.

**Permissions & sessions:** which browser session an MCP client drives, and which origins it is allowed to act on, are governed by the E2LLM permission / auth-session model. Know whose session you are operating before you act.

**Find and read** — > Open <url>, read the main article with read_page, and give me the key claims, each with the sentence it is based on.

**Fill and submit a form** — > Fill the contact form (name: …, email: …, message: …) and submit. Use query to locate fields, then batch_act to fill + submit in one pass. Show me what you will submit and wait for my OK before sending.

**Multi-step navigation** — > From the dashboard, find the most recent invoice, open it, tell me the total. query + act to navigate, read_page to extract.

**Inspect before acting (safety)** — > Before clicking anything, use inspect on the "Delete account" button and tell me exactly what it targets. Do NOT act until I confirm.

**Tab hygiene** — > list_tabs; close the search-result tabs with close_tab, keep the article tabs.

### Day-2 / robustness recipes
Real pages fail in real ways — prompt for it:
- **Element not found / action failed** — > Click "Export". If query returns no match or act reports a failure, tell me what you actually see on the page instead of retrying blindly — the label or state may have changed.
- **Partial batch_act (mid-batch failure)** — > Fill this 6-field form with batch_act. If any step fails, STOP, report which step and why, and do NOT submit a half-filled form.
- **Pagination / infinite scroll** — > Collect all results across pages. After reading each page, act Next (or scroll to load more); stop when no new items appear or after N pages, and give me the count.
- **Dynamic content** — > This page loads content after a delay. Capture, and if the section I asked about is empty, wait/scroll and re-capture before answering rather than reporting "not present".

## Which one am I using? (quick self-check)
- "I clicked the extension and copied some text" -> **E2LLM**.
- "My AI assistant opened a page and clicked a button" -> **E2LLM MCP**.
- "I want the model to *read* one page" -> either; E2LLM is simpler.
- "I want the model to *do* a multi-step task in the browser" -> **E2LLM MCP**.

## About this repo
A practical **cookbook** of prompt recipes. Put extension/SiFR-capture recipes under E2LLM and MCP/tool-use recipes under E2LLM MCP — keeping the two surfaces separate is the point.
