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

## Security Audit Summary (March 2026)

A full security review was conducted on the codebase. Key findings and mitigations:

### Known Architectural Trade-offs (Not Vulnerabilities)

- **Babel Standalone / `unsafe-eval`**: JSX is compiled at runtime. This requires `unsafe-eval` in the Content Security Policy. For higher-security deployments, pre-compile JSX with the Babel CLI or Vite to eliminate this attack surface entirely.
- **Tailwind Play CDN / `unsafe-inline`**: The Tailwind CDN generates CSS dynamically and does not support Subresource Integrity (SRI). Use the Tailwind CLI for production builds.
- **CDN scripts without SRI hashes**: React 18.3.1 and Babel 7.26.4 are loaded from unpkg.com without SRI verification. To add SRI, download each file and compute: `openssl dgst -sha384 -binary <file> | openssl base64 -A`, then add as `integrity="sha384-<hash>"` attributes. Tailwind CDN does not support SRI.
- **Google Fonts**: Loading Inter from `fonts.googleapis.com` / `fonts.gstatic.com` creates a connection to Google's servers. Self-host the font files to eliminate this dependency.

### Mitigations Applied

- **Content Security Policy**: Declared via `<meta http-equiv>` with `connect-src 'none'` (no external API calls), `object-src 'none'`, `base-uri 'self'`, and `frame-ancestors 'none'` (clickjacking protection).
- **External links**: All `target="_blank"` links include `rel="noopener noreferrer"` to prevent tab-napping.
- **No `dangerouslySetInnerHTML`**: React renders report content via safe component parsing only.
- **No persistent storage**: No `localStorage`, `sessionStorage`, cookies, or server-side storage. All data is ephemeral in memory.
- **No hardcoded secrets**: No API keys, tokens, or credentials in source.

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

## License

This project is licensed under the [Apache License 2.0](LICENSE).
