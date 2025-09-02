# Contributing to Awesome E2LLM Prompts

Thanks for your interest in contributing! 🚀  
This repository is a curated collection of prompts for [Element to LLM (E2LLM)](https://insitu.im/e2llm/).

---

## 📝 How to contribute

1. **Fork** the repo and create a new branch.
2. Add or edit prompts in `README.md` (or propose new categories if relevant).
3. Use clear formatting:
   - Category (Debugging, UX Analysis, Interaction & Focus, Automation, Code Review)
   - Prompt title (short and descriptive)
   - Prompt code block with `{E2LLM_JSON}` placeholder
   - Example / expected output (if possible)
4. Submit a **Pull Request** with a short explanation of what you added/changed.

---

## ✅ Prompt Guidelines

- Must be directly useful with E2LLM JSON snapshots.
- Keep prompts practical (debugging, QA, UX, frontend workflows).
- Use `{E2LLM_JSON}` as a placeholder instead of real code when possible.
- Be concise but clear. Add bullet points for checks/criteria if helpful.
- Avoid marketing language — focus on technical value.

---

## 🐛 Reporting Issues

- Use **Issues** tab to report bugs or suggest improvements.
- For new prompt ideas, open an issue with label `prompt-suggestion`.

---

## 📖 Example format

### 🐛 Debugging

**Form Debugging**
```
This form isn't working properly. Analyze the DOM state:
{E2LLM_JSON}

Check:
- Required field validation
- Input types and constraints
- Disabled/hidden elements
```

---

## 🙌 Community Rules

- Be respectful and constructive.
- Keep contributions focused on prompts, QA, debugging, and frontend workflows.
- By contributing, you agree your content will be published under the MIT License.
