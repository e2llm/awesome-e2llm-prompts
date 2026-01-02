# QA & Regression Detection Prompts

Detect UX regressions that pass functional tests but break user experience.

## Bug Report Analysis

```
Analyze this SiFR snapshot. The user reports: "{bug_description}"

Identify:
1. Root cause (disabled attribute? CSS conflict? JS state?)
2. Affected elements (provide selectors)
3. Why the element appears functional but isn't working
4. Suggested fix with code example

{E2LLM_JSON}
```

## Semantic Regression Check

```
You're monitoring a web page for UX regressions.
Recent semantic snapshots (oldest to newest):

[1]: {previous_state_1}
[2]: {previous_state_2}
[3]: {current_state}

Questions:
1. Is the latest snapshot a regression from established baseline?
2. Are primary actions (CTAs, forms, checkout) still accessible and prominent?
3. Is any critical UI element hidden, pushed off-screen, or covered?

Reply: {regression: true/false, severity: "critical/warning/none", reason: "..."}
```

## Functional State Description

```
Describe this page's functional state:
{E2LLM_JSON}

Report:
1. Primary actions available (buttons, forms, CTAs)
2. Content hierarchy (what's prominent vs hidden)
3. Any UI issues (overlaps, off-screen elements, broken layout)

Be consistent. Same functional state = same description.
```

## Multi-Viewport Regression

```
Compare semantic states across viewports:

Desktop (1920x1080): {desktop_state}
Tablet (768x1024): {tablet_state}
Mobile (375x667): {mobile_state}

Report responsive regressions where mobile/tablet UX is degraded vs desktop.
Focus on: CTA visibility, content accessibility, touch target sizes.
```

## Layout Overlap Detection

```
Analyze this SiFR snapshot for layout/UX issues:
{E2LLM_JSON}

Check for:
- HIGH salience interactive elements being overlapped by other elements
- Elements marked interactive:false that should be clickable
- Fixed/absolute positioned elements covering main content
- Z-index conflicts where popups/banners block CTAs

Return: {issues: [{element, overlappedBy, severity}]}
```

## Usage

These prompts are designed for:
- Post-deploy regression detection
- CI/CD pipeline integration
- Scheduled monitoring (hourly/daily)
- Multi-viewport responsive testing

See [Runtime Snapshots #9](https://dev.to/anthropics/runtime-snapshots-9-semantic-regression-detection) for implementation details.
