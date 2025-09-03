# Awesome E2LLM Prompts

![GitHub stars](https://img.shields.io/github/stars/e2llm/awesome-e2llm-prompts?style=social)
![License](https://img.shields.io/github/license/e2llm/awesome-e2llm-prompts)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

**Keywords:** DOM snapshot, LLM debugging, runtime DOM analysis, element inspection, web debugging prompts, e2llm
> Curated prompts for LLM debugging with runtime DOM snapshots. Transform live DOM state into structured JSON for better AI analysis.

**Element to LLM** captures live DOM snapshot and exports structured JSON that LLMs can reason over. This repo contains battle-tested prompts to get the most out of your DOM snapshots.

⭐ If you find this useful, give the repo a star — it helps others discover it.
## 🔗 Get the Extension
- [Chrome Web Store](https://chromewebstore.google.com/detail/element-to-llm/oofdfeinchhgnhlikkfdfcldbpcjcgnj)
- [Firefox Add-ons](https://addons.mozilla.org/firefox/addon/element-to-llm/)

## 📚 Categories

### 🐛 DOM Debugging
Find and fix UI issues faster with structured DOM context.

**Basic Bug Analysis**
Analyze this DOM snapshot for potential issues:
{E2LLM_JSON}

Look for:

Missing labels or unclear naming

Layout issues (overflow, positioning problems)

Form validation errors

Excessive nesting or unused styles

Provide specific recommendations with CSS/HTML fixes.

css
Copy code

**Form Debugging**
This form isn't working properly. Analyze the DOM state:
{E2LLM_JSON}

Check:

Required field validation

Input types and constraints

Disabled/hidden elements

Event handlers and form action

Label-input associations

What's preventing form submission?

markdown
Copy code

**CSS Layout Issues**
Elements aren't positioning correctly. Debug this layout:
{E2LLM_JSON}

Examine:

Flexbox/Grid properties and container relationships

Z-index conflicts

Margin collapse issues

Overflow problems

Viewport-relative units

Suggest specific CSS fixes.

yaml
Copy code

---

### 🎨 UX Analysis
Get AI-powered insights on user experience and interface design.

**UX Audit**
Perform a UX audit on this interface element:
{E2LLM_JSON}

Evaluate:

Information hierarchy and visual weight

User flow and interaction patterns

Clarity of structure

Mobile responsiveness indicators

Error handling and recovery

Rate each area 1–10 and suggest improvements.

pgsql
Copy code

**Conversion Optimization**
Analyze this UI element for conversion optimization:
{E2LLM_JSON}

Focus on:

Call-to-action visibility and placement

Form friction and field requirements

Trust signals

Loading states and responsiveness

Mobile experience quality

What changes would likely improve conversion rates?

yaml
Copy code

---

### 🎯 Interaction & Focus
Check how interactive elements behave in real use.

**Focus Management**
Analyze focus management for this interactive element:
{E2LLM_JSON}

Evaluate:

Tab order and navigation flow

Focus indicators and visibility

Skip links or jump points

Modal/dialog focus trapping

Dynamic content updates

How can focus handling be improved?

pgsql
Copy code

**Role & Structure Check**
Inspect this JSON snapshot and identify missing or incorrect roles/attributes:
{E2LLM_JSON}

Highlight:

Structural clarity

Naming conventions

Logical grouping

Attribute use that improves clarity

yaml
Copy code

---

### 🤖 Test Automation & Selectors
Generate reliable selectors and test scenarios.

**Stable Selectors**
Generate robust CSS selectors for test automation:
{E2LLM_JSON}

Create selectors that:

Don't rely on brittle class names or IDs

Use semantic attributes and structure

Are resilient to style changes

Work across different screen sizes

Follow automation best practices

Provide Playwright/Cypress examples.

markdown
Copy code

**Test Scenario Generation**
Generate test scenarios for this UI element:
{E2LLM_JSON}

Include:

Happy path user interactions

Edge cases and error conditions

Cross-browser considerations

Mobile-specific behaviors

Performance checkpoints

Write test descriptions in Gherkin format.

yaml
Copy code

---

### 🔍 Code Review
AI-powered code review for frontend components.

**HTML/CSS Review**
Review this DOM structure and styles for best practices:
{E2LLM_JSON}

Assess:

Semantic HTML usage

CSS organization and specificity

Performance implications

Maintainability concerns

Browser compatibility issues

Provide refactoring recommendations.

markdown
Copy code

---

## 💡 Pro Tips

### Getting Better Results
1. **Be specific** — Target the exact element causing issues  
2. **Add context** — Mention the user flow or expected behavior  
3. **Request examples** — Ask for code samples, not just explanations  
4. **Iterate** — Use follow-up prompts to drill deeper  

### Prompt Templates
Replace `{E2LLM_JSON}` with your actual DOM snapshot. Most prompts work best with elements that have interactive behavior or visual complexity.

### Integration Examples

**With Playwright**
```javascript
// Capture element before test
await page.click('#capture-btn');
// Get E2LLM JSON from clipboard
const domSnapshot = await page.evaluate(() => navigator.clipboard.readText());
// Send to LLM for analysis
With Development Workflow

bash
Copy code
# Capture → Analyze → Fix → Verify
1. Use E2LLM on problematic element
2. Paste JSON into ChatGPT/Claude with prompt
3. Implement suggested fixes
4. Capture again to verify improvement
📖 Examples
Real DOM Snapshot Example

json
Copy code
{
  "targetElement": {
    "selector": "form.login-form",
    "tag": "form",
    "classes": ["login-form", "card"],
    "computedStyles": {
      "layout": {"width": "400px", "height": "300px"},
      "typography": {"font-family": "Arial, sans-serif"}
    },
    "children": [...]
  }
}
```
Before/After Results

Before: "The login form looks broken"

After: "The form validation is failing because the email input has type="text" instead of type="email", and the required attribute isn't set on the password field."

### 🤝 Contributing

 ## Add your proven prompts! Submit a PR with:
Clear category and use case
Example JSON input (anonymized)
Expected output quality
Real-world context where it helped

### 📝 License
MIT — Use these prompts however helps your workflow.

### 🔗 Related
Element to LLM Extension

- [Chrome Web Store](https://chromewebstore.google.com/detail/element-to-llm/oofdfeinchhgnhlikkfdfcldbpcjcgnj)
- [Firefox Add-ons](https://addons.mozilla.org/firefox/addon/element-to-llm/)

Runtime DOM snapshots > static code. Debug smarter, not harder.

## 🔍 Search Terms
Find this repo by searching: `dom debugging llm`, `runtime dom json`, `element snapshot prompts`
