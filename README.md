# Awesome E2LLM Prompts

[![GitHub stars](https://img.shields.io/github/stars/e2llm/awesome-e2llm-prompts?style=social)](https://github.com/e2llm/awesome-e2llm-prompts)
[![License](https://img.shields.io/github/license/e2llm/awesome-e2llm-prompts)](LICENSE)
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated prompts for debugging, testing, and monitoring with runtime DOM snapshots.

**Element to LLM** captures live DOM state as structured JSON (SiFR format) that LLMs can reason over. This repo contains battle-tested prompts organized by use case.

## Get the Extension

- [Chrome Web Store](https://chromewebstore.google.com/detail/element-to-llm/oofdfeinchhgnhlikkfdfcldbpcjcgnj)
- [Firefox Add-ons](https://addons.mozilla.org/firefox/addon/element-to-llm/)

---

## Categories

| Category | Use Case |
|----------|----------|
| [DOM Debugging](#-dom-debugging) | Find and fix UI bugs |
| [UX Analysis](#-ux-analysis) | Audit user experience |
| [Interaction & Focus](#-interaction--focus) | Check interactive behavior |
| [Test Automation](#-test-automation--selectors) | Generate selectors and scenarios |
| [Code Review](#-code-review) | Review HTML/CSS quality |
| [QA & Regression](#-qa--regression-detection) | Detect UX regressions |
| [Security Monitoring](#-security-monitoring) | Detect defacement and overlays |

---

### 🐛 DOM Debugging

**Basic Bug Analysis**
```
Analyze this DOM snapshot for potential issues:
{E2LLM_JSON}

Look for:
- Missing labels or unclear naming
- Layout issues (overflow, positioning)
- Form validation errors
- Excessive nesting

Provide specific CSS/HTML fixes.
```

**Form Debugging**
```
This form isn't working. Analyze the DOM state:
{E2LLM_JSON}

Check:
- Required field validation
- Input types and constraints
- Disabled/hidden elements
- Label-input associations

What's preventing submission?
```

**CSS Layout Issues**
```
Elements aren't positioning correctly:
{E2LLM_JSON}

Examine:
- Flexbox/Grid properties
- Z-index conflicts
- Margin collapse
- Overflow problems

Suggest specific CSS fixes.
```

---

### 🎨 UX Analysis

**UX Audit**
```
Perform a UX audit:
{E2LLM_JSON}

Evaluate:
- Information hierarchy
- User flow patterns
- Mobile responsiveness
- Error handling

Rate each area 1-10 with improvements.
```

**Conversion Optimization**
```
Analyze for conversion optimization:
{E2LLM_JSON}

Focus on:
- CTA visibility and placement
- Form friction
- Trust signals
- Mobile experience

What would improve conversion?
```

---

### 🎯 Interaction & Focus

**Focus Management**
```
Analyze focus management:
{E2LLM_JSON}

Evaluate:
- Tab order and flow
- Focus indicators
- Modal focus trapping
- Dynamic content updates

How can focus handling improve?
```

**Role & Structure Check**
```
Identify missing or incorrect roles/attributes:
{E2LLM_JSON}

Highlight:
- Structural clarity
- Naming conventions
- Logical grouping
```

---

### 🤖 Test Automation & Selectors

**Stable Selectors**
```
Generate robust CSS selectors for automation:
{E2LLM_JSON}

Create selectors that:
- Don't rely on brittle classes/IDs
- Use semantic attributes
- Are resilient to style changes
- Work across screen sizes

Provide Playwright/Cypress examples.
```

**Test Scenario Generation**
```
Generate test scenarios:
{E2LLM_JSON}

Include:
- Happy path interactions
- Edge cases and errors
- Mobile-specific behaviors

Write in Gherkin format.
```

---

### 🔍 Code Review

**HTML/CSS Review**
```
Review this DOM structure for best practices:
{E2LLM_JSON}

Assess:
- Semantic HTML usage
- CSS organization
- Performance implications
- Browser compatibility

Provide refactoring recommendations.
```

---

### 🔬 QA & Regression Detection

Detect UX regressions that pass functional tests but break user experience.

**Bug Report Analysis**
```
Analyze this SiFR snapshot. User reports: "{bug_description}"

Identify:
1. Root cause (disabled attr? CSS conflict? JS state?)
2. Affected elements (selectors)
3. Why element appears functional but isn't working
4. Suggested fix with code

{E2LLM_JSON}
```

**Semantic Regression Check**
```
You're monitoring for UX regressions.
Recent semantic snapshots (oldest to newest):

[1]: {previous_state_1}
[2]: {previous_state_2}
[3]: {current_state}

Questions:
1. Is latest snapshot a regression from baseline?
2. Are primary actions (CTAs, forms) still accessible?
3. Is any critical UI hidden, off-screen, or covered?

Reply: {regression: true/false, severity: "critical/warning/none", reason: "..."}
```

**Functional State Description**
```
Describe this page's functional state:
{E2LLM_JSON}

Report:
1. Primary actions available (buttons, forms, CTAs)
2. Content hierarchy (prominent vs hidden)
3. Any UI issues (overlaps, off-screen, broken layout)

Be consistent. Same state = same description.
```

**Multi-Viewport Regression**
```
Compare semantic states across viewports:

Desktop (1920x1080): {desktop_state}
Tablet (768x1024): {tablet_state}
Mobile (375x667): {mobile_state}

Report responsive regressions where mobile/tablet UX is degraded.
Focus on: CTA visibility, content accessibility, touch targets.
```

**Layout Overlap Detection**
```
Analyze for layout/UX issues:
{E2LLM_JSON}

Check for:
- HIGH salience elements being overlapped
- Elements marked interactive:false that should be clickable
- Fixed/absolute elements covering main content
- Z-index conflicts where popups block CTAs

Return: {issues: [{element, overlappedBy, severity}]}
```

---

### 🛡️ Security Monitoring

Detect defacement, malicious overlays, and content injection.

**Defacement Detection**
```
Compare this snapshot against expected content for a {site_type} site:
{E2LLM_JSON}

Red flags:
- Unexpected adult/violent/political keywords in HIGH salience text
- Images from external/unknown domains
- Drastic structure change
- Suspicious iframes or scripts
- Foreign language where shouldn't be

Return: {compromised: true/false, severity: 1-10, evidence: [...]}
```

**Phishing Overlay Detection**
```
Analyze for malicious overlays:
{E2LLM_JSON}

Check for:
- New high-salience forms over existing login
- Duplicate authentication elements
- Suspicious iframe covering critical areas
- Form actions pointing to external domains
- Hidden input fields capturing credentials

Flag anomalies with selectors.
```

**Content Integrity Check**
```
You are a security monitor. Analyze semantic state:
{E2LLM_JSON}

Expected site type: {expected_type}

Verify:
1. Content matches expected site purpose
2. No injected spam content
3. Navigation structure intact
4. Critical elements unmodified

Report: {integrity: "ok/warning/compromised", issues: [...]}
```

---

## Pro Tips

1. **Be specific** — Target the exact element causing issues
2. **Add context** — Mention the user flow or expected behavior
3. **Request examples** — Ask for code samples, not explanations
4. **Iterate** — Use follow-up prompts to drill deeper

Replace `{E2LLM_JSON}` with your actual DOM snapshot.

---

## Integration

**Playwright**
```javascript
const sifr = await page.evaluate(() => {
  return new Promise((resolve) => {
    document.addEventListener('e2llm-capture-response', (e) => {
      resolve(e.detail.data);
    }, { once: true });
    document.dispatchEvent(new CustomEvent('e2llm-capture-request', {
      detail: { selector: 'body', options: { preset: 'normal' } }
    }));
  });
});
```

---

## Contributing

Add your proven prompts! Submit a PR with:
- Clear category and use case
- Example JSON input (anonymized)
- Real-world context where it helped

## License

MIT

---

**Related:** [Runtime Snapshots Series on Dev.to](https://dev.to/anthropics)
