---
title: "Thousands of AI-Built Apps Are Leaking Corporate and Personal Data on the Open Web"
source_url: "https://www.wired.com/story/thousands-of-vibe-coded-apps-expose-corporate-and-personal-data-on-the-open-web/"
publication_date: "2026-05-07"
keyword_match: "Coding agents; AI governance tension; enterprise AI adoption gap"
---

## Title
Thousands of AI-Built Apps Are Leaking Corporate and Personal Data on the Open Web

## Source URL
https://www.wired.com/story/thousands-of-vibe-coded-apps-expose-corporate-and-personal-data-on-the-open-web/

## Publication Date
May 7, 2026

## Keyword Match
- Coding agents and pattern-bound vs. judgment-heavy work (Keyword #3)
- AI governance, federal vs. state regulatory tension (Keyword #7)
- Enterprise AI adoption gap — usage without ROI (Keyword #8)

## Summary
Security researcher Dor Zvi and his team at RedAccess analyzed thousands of web applications built with AI coding tools — Lovable, Replit, Base44, and Netlify — and found more than 5,000 that had virtually no security or authentication of any kind. Around 40 percent of those exposed sensitive data, including medical records, financial information, corporate strategy documents, customer chatbot logs with full names and contact details, and cargo records. The researchers found phishing sites impersonating Bank of America, Costco, FedEx, and McDonald's hosted on Lovable's own domain. The companies involved pushed back on claims and noted users are responsible for their own security settings. But security researchers and the article confirm the core pattern: non-technical employees — marketers, ops leads, founders — are spinning up production-grade apps using AI tools without any security review, and those apps are live on the internet with no guardrails. The root cause is structural: AI coding tools enable a new class of app creators who operate entirely outside normal software development cycles.

## Key Data Points
- 5,000+ AI-built web apps left publicly accessible with no authentication (found via simple Google/Bing searches)
- ~40% of those apps exposed sensitive data: medical PII, financial records, corporate strategy docs, customer chatbot logs
- Phishing sites impersonating Bank of America, Costco, FedEx, Trader Joe's, McDonald's found hosted on Lovable's domain
- Platforms affected: Lovable, Replit, Base44 (owned by Wix), and Netlify
- Apps hosted on AI companies' own domains, making them trivially discoverable via search
- RedAccess compared the exposure wave to the Amazon S3 misconfiguration epidemic of earlier years
- Researcher quote: "Anyone from your company at any moment can generate an app, and this is not going through any development cycle or any security check"
- Replit CEO Amjad Masad: "Public apps being accessible on the internet is expected behavior"
- Lovable: "How an app is configured is ultimately the creator's responsibility"
- The 5,000 apps found are only those on AI company domains; likely thousands more on custom domains remain undiscovered

## Why It Matters
This is a direct warning for any SMB or team lead whose staff use AI coding tools to build internal apps, dashboards, or customer-facing tools. The risk is not just theoretical — researchers confirmed real corporate data exposure in multiple cases. The story reframes "vibe coding" from a productivity win into a governance liability if there is no process for reviewing what gets deployed. Founders and operations leads need to ask today: who on my team is using Lovable, Replit, or Base44, what have they built, and is it publicly accessible? The Wix/Base44 response effectively puts the liability entirely on the user. This is the same pattern that burned thousands of companies with misconfigured S3 buckets — but faster and with a wider blast radius because AI tools lower the skill floor for deployment.

## Related Themes
Vibe coding, AI security, coding agents, no-code AI, data exposure, enterprise governance, AI risk, shadow IT, SMB security, Lovable, Replit, Base44, Netlify