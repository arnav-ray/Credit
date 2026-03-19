# Security Policy

## Scope

OpenCredit Platform is a **client-side-only** educational tool. All calculations run entirely in the user's browser. No user data is transmitted to any server, stored in a database, or shared with third parties.

## Supported Versions

| Version | Supported |
|---------|-----------|
| Latest (main branch) | Yes |
| Older commits | No — please update to latest |

## Reporting a Vulnerability

If you discover a security issue in this project, please report it responsibly:

- **Email:** arnav@arnavray.ca
- **Subject line:** `[OpenCredit Security]`
- **Response time:** We aim to acknowledge reports within 72 hours.

Please include:
1. A description of the vulnerability and its potential impact
2. Steps to reproduce
3. Any relevant browser/OS version information

We ask that you do **not** publicly disclose the issue until we have had a reasonable opportunity to investigate and release a fix.

## Known Non-Issues

The following are known architectural trade-offs, not vulnerabilities:

- **Babel Standalone in browser**: JSX is compiled at runtime. This requires `unsafe-eval` in the Content Security Policy. For higher-security deployments, pre-compile JSX with the Babel CLI or Vite.
- **Tailwind Play CDN**: The Tailwind CDN generates CSS dynamically and does not support Subresource Integrity (SRI). Use the Tailwind CLI for production builds.
- **Google Fonts**: Loading Inter font from `fonts.googleapis.com` / `fonts.gstatic.com` creates a connection to Google's servers. If this is undesirable, self-host the font files instead.

## Data Privacy

- No personal data ever leaves your browser.
- No cookies are set.
- No analytics, tracking pixels, or third-party data collectors are used.
- The only external connections are: CDN libraries (React, Babel, Tailwind) and Google Fonts.

## Third-Party Dependencies

| Library | Version | Source |
|---------|---------|--------|
| React | 18.3.1 | unpkg.com |
| ReactDOM | 18.3.1 | unpkg.com |
| Babel Standalone | 7.26.4 | unpkg.com |
| Tailwind CSS | Latest (Play CDN) | cdn.tailwindcss.com |
| Inter font | Latest | fonts.googleapis.com |

To verify integrity of pinned CDN scripts, download each file and compute:
```
openssl dgst -sha384 -binary <file> | openssl base64 -A
```
Then add the resulting hash as an `integrity="sha384-<hash>"` attribute on each `<script>` tag.
