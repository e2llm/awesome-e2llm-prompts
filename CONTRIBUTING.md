# Contributing to Awesome E2LLM Prompts

Thanks for your interest in contributing! 🚀  
This repository is a **cookbook of prompt recipes** for the [Element to LLM (E2LLM)](https://insitu.im/e2llm/) family — turning any web page into something an LLM can *read* (the **E2LLM** extension captures the page as **SiFR**), and any web UI into something an agent can *operate* (**E2LLM MCP** exposes the browser as tools).

Recipes are organized by those two surfaces — keeping them separate is the point.

---

## 📝 How to contribute

1. **Fork** the repo and create a new branch.
2. Add or edit recipes in `README.md`, under the section they belong to:
   - **E2LLM (capture) recipes** — a human captures the page as SiFR and pastes it into an LLM (perception: summarize, extract, compare, answer-from-page).
   - **E2LLM MCP (tool-use) recipes** — an MCP client drives the browser; the model perceives *and* acts (find, read, fill, navigate, multi-step).
   - **Day-2 / robustness recipes** — real-page failure modes: missing elements, partial batches, pagination / infinite scroll, dynamic content.
3. Match the existing **recipe format** (below).
4. Open a **Pull Request** with a one-line explanation of what you added or changed.

---

## ✅ Recipe guidelines

- **Stay capability-grounded — do not invent features.** Use only what E2LLM actually does: real SiFR capture behavior, and the real MCP tools — `query`, `inspect`, `read_page`, `sifr_capture`, `act`, `batch_act`, `explore`, `list_tabs`, `close_tab`. No imaginary tools, flags, or options.
- **Put the recipe on the right surface.** If a *human* pastes page content into a chat → **E2LLM**. If the *model* operates the UI itself → **E2LLM MCP**.
- **Talk about SiFR, not raw HTML.** For capture recipes, say "here is a SiFR capture" and, where useful, point at SiFR sections (SUMMARY, NODES, RELATIONS) instead of pasting real markup.
- **Build in safety for actions.** For anything destructive or irreversible, the recipe should have the model `inspect` first and wait for confirmation before it acts.
- **Keep it practical and concise.** A short title and the prompt; add bullet checks only when they earn their place. Skip marketing language — focus on technical value.

---

## 📖 Recipe format

Give the recipe a short **bold title**, then the prompt, under the right section:

**Extract structured data** — > From this SiFR capture, extract every product as JSON {name, price, rating}. Use NODES + RELATIONS to resolve which value belongs to which product.

For E2LLM MCP recipes, name the tools the recipe expects:

**Fill and submit a form** — > Fill the contact form (name, email, message) and submit. Use query to locate the fields, then batch_act to fill + submit in one pass — show me what you'll submit and wait for my OK before sending.

---

## 🐛 Reporting issues & suggesting recipes

- Use the **Issues** tab to report a problem or suggest an improvement.
- For a new recipe idea, open an issue with the **`prompt-suggestion`** label.

---

## 🙌 Community rules

- Be respectful and constructive.
- Keep contributions focused on E2LLM prompt recipes — SiFR capture and MCP tool-use.
- By contributing, you agree your content will be published under the MIT License.
