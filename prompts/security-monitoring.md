# Security Monitoring Prompts

Detect defacement, malicious overlays, and content injection.

## Defacement Detection

```
Compare this SiFR snapshot against expected content for a {site_type} site.
{E2LLM_JSON}

Red flags to detect:
- Unexpected adult/violent/political keywords in HIGH salience text
- Images from external/unknown domains
- Drastic structure change (normal site has nav+content+footer)
- Suspicious iframes or scripts in attributes
- Foreign language where shouldn't be
- SEO spam or hidden text

Return: {compromised: true/false, severity: 1-10, evidence: [...]}
```

## Phishing Overlay Detection

```
Analyze this SiFR snapshot for malicious overlays:
{E2LLM_JSON}

Check for:
- New high-salience forms appearing over existing login
- Duplicate authentication elements
- Suspicious iframe covering critical areas
- Form actions pointing to external domains
- Hidden input fields capturing credentials

Flag anomalies with element selectors.
```

## Content Integrity Check

```
You are a security monitor. Analyze semantic state:
{E2LLM_JSON}

Expected site type: {expected_type} (e.g., e-commerce, corporate, blog)

Verify:
1. Content matches expected site purpose
2. No injected promotional/spam content
3. Navigation structure intact
4. Critical elements (login, checkout) unmodified

Report: {integrity: "ok/warning/compromised", issues: [...]}
```

## Why Salience Matters for Security

SiFR captures salience scores for each element. This means:

- **Defacement attacks** typically replace HIGH salience content (visible, prominent)
- **Phishing overlays** create new HIGH salience forms over existing ones
- **SEO spam injection** often targets LOW salience areas (hidden text, footers)

The LLM focuses on what matters — high-salience changes trigger alerts, low-salience noise is ignored.

## Usage

These prompts are designed for:
- Scheduled security monitoring
- Post-incident forensics
- Third-party script auditing
- Content injection detection

See [Runtime Snapshots #9](https://dev.to/anthropics/runtime-snapshots-9-semantic-regression-detection) for implementation details.
