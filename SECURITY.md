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

## Deployment

The platform is deployed via **Vercel**. HTTP security headers are enforced server-side via `vercel.json`:

| Header | Value |
|--------|-------|
| `Strict-Transport-Security` | `max-age=31536000; includeSubDomains; preload` |
| `X-Content-Type-Options` | `nosniff` |
| `X-Frame-Options` | `DENY` |
| `Referrer-Policy` | `strict-origin-when-cross-origin` |

The in-page Content Security Policy (`<meta http-equiv="Content-Security-Policy">`) additionally enforces:

| Directive | Value | Purpose |
|-----------|-------|---------|
| `default-src` | `'self'` | Blocks all unlisted sources by default |
| `connect-src` | `'none'` | Prevents all outbound API calls — no data exfiltration possible |
| `object-src` | `'none'` | Blocks Flash and other plugin content |
| `base-uri` | `'self'` | Prevents base tag injection |
| `frame-ancestors` | `'none'` | Blocks iframe embedding / clickjacking |

## Known Architectural Trade-offs

The following are deliberate trade-offs for a CDN-hosted, build-tooling-free deployment. They are not exploitable vulnerabilities in the current threat model (client-side only, no sensitive server state), but would need to be resolved before any production backend integration.

### Babel Standalone / `unsafe-eval`
JSX is compiled at runtime in the browser by Babel Standalone. This requires `unsafe-eval` in the CSP, which significantly weakens its XSS protections. **For higher-security deployments**, pre-compile JSX with the Babel CLI or Vite and remove this dependency entirely.

### Tailwind Play CDN / `unsafe-inline`
The Tailwind CDN injects styles dynamically and does not support Subresource Integrity (SRI). This requires `unsafe-inline` in `style-src`. **For production**, use the Tailwind CLI to generate a static CSS bundle with an SRI hash.

### CDN Scripts Without SRI Hashes
React 18.3.1, ReactDOM 18.3.1, and Babel Standalone 7.26.4 are loaded from `unpkg.com` without `integrity=` attributes. A compromised CDN or BGP hijack could inject malicious code. To add SRI:

```sh
openssl dgst -sha384 -binary <downloaded-file> | openssl base64 -A
```

Then add `integrity="sha384-<hash>"` to each `<script>` tag. Note: Tailwind's Play CDN does not support SRI.

### Google Fonts
The Inter typeface is loaded from `fonts.googleapis.com` / `fonts.gstatic.com`. This creates a connection to Google's servers on each page load, which has privacy implications (Google receives referrer data). To eliminate this dependency, self-host the Inter font files.

## Security Practices in Place

- **No `dangerouslySetInnerHTML`**: All dynamic content is rendered via safe React component parsing.
- **No persistent storage**: No `localStorage`, `sessionStorage`, cookies, or server-side storage. All state is ephemeral in browser memory.
- **No hardcoded secrets**: No API keys, tokens, or credentials anywhere in the source.
- **All external links** use `rel="noopener noreferrer"` on `target="_blank"` to prevent tab-napping.
- **Error boundary**: A React `ErrorBoundary` wraps the entire application to prevent unhandled render errors from exposing internal state to the user.

## Data Privacy

- No personal data ever leaves your browser.
- No cookies are set.
- No analytics, tracking pixels, or third-party data collectors are used.
- External connections are limited to: CDN delivery of React, Babel, and Tailwind; and Google Fonts.

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
