---
source_file: content/research/2026-02-25-firefox-148-sethtml-sanitizer-api.md
status: ranked
created_date: 2026-02-25
---

innerHTML has been a security liability since before some of your junior devs were born. Firefox 148 just handed us the exit ramp.

Firefox shipped the standardized Sanitizer API this week — the first browser to do so — introducing `setHTML()` as a secure, built-in replacement for the notorious `innerHTML`. The difference: `setHTML()` automatically strips dangerous elements and attributes before anything touches the DOM. Security by default. No extra libraries. Minimal code changes.

XSS has been in the OWASP Top 3 web vulnerabilities for nearly a decade. A significant chunk of that is directly attributable to developers using `innerHTML` with untrusted input — not because they're bad engineers, but because the safe alternative didn't exist at the platform level. It does now.

The API also integrates with Trusted Types for layered enforcement, supports custom sanitization configs for teams that need stricter or more permissive rules, and has a playground available for testing before you touch production.

Mozilla also pioneered Content Security Policy back in 2009, which saw notoriously slow adoption due to implementation complexity. The Sanitizer API is explicitly designed to avoid that fate — accessible to devs at every experience level, not just security specialists.

If `innerHTML` is still in your codebase touching user input, this is your sign. The platform just made the right thing the easy thing.

#WebDevelopment #Cybersecurity #Firefox #JavaScript #XSS
