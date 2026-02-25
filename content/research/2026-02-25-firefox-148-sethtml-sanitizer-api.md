# Firefox 148 Ships Sanitizer API with setHTML — A Major Step Forward for Web XSS Security

**Title:** Goodbye innerHTML, Hello setHTML: Stronger XSS Protection in Firefox 148

**Source URL:** https://hacks.mozilla.org/2026/02/goodbye-innerhtml-hello-sethtml-stronger-xss-protection-in-firefox-148/

**Publication Date:** February 24, 2026

**Summary:**
Firefox 148 becomes the first browser to ship the standardized Sanitizer API, introducing the `setHTML()` method as a secure, built-in replacement for the widely-used but vulnerability-prone `innerHTML`. Cross-site scripting (XSS) has ranked among the top three web security risks for nearly a decade, and `innerHTML` is a primary contributor — it inserts untrusted HTML into the DOM without any sanitization. The new `setHTML()` method automatically strips dangerous elements and attributes before DOM insertion, providing security by default with minimal code changes required from developers. Firefox pioneered Content Security Policy (CSP) back in 2009, but CSP saw limited adoption due to architectural complexity; the Sanitizer API is designed to be accessible to developers of all experience levels. The API also integrates with the Trusted Types framework for layered security enforcement.

**Key Data Points:**
- Firefox 148 is the first browser to ship the standardized Sanitizer API
- XSS has been in the OWASP Top 3 web vulnerabilities for nearly a decade
- `setHTML()` strips dangerous elements/attributes before DOM insertion — security by default
- Supports custom configurations for stricter or more permissive sanitization
- Integrates with the Trusted Types API for enhanced security layers
- Developers can test the feature at the Sanitizer API playground before production use
- Mozilla also pioneered Content Security Policy (CSP) in Firefox in 2009

**Why It Matters:**
XSS vulnerabilities remain one of the most exploited classes of web security bugs, costing organizations significant remediation effort and reputational damage. The Sanitizer API's arrival in Firefox 148 gives web developers a standards-based, low-friction path to eliminate an entire category of injection vulnerabilities. For engineering teams, this is both an immediate security upgrade opportunity and a signal of the browser security baseline shifting upward. Product and security leaders should ensure their development teams are aware of this API and begin planning migration away from raw `innerHTML` usage.

**Related Themes:**
Cybersecurity, web development, Firefox, browser security, XSS, Sanitizer API, JavaScript, developer tools, open web standards
