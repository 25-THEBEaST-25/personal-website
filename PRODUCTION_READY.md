# Production Readiness Checklist

Status: **Complete**

| Requirement | Status |
|---|---|
| CSP, OG tags, favicon, robots.txt, sitemap.xml, WCAG contrast fix | Done (prior session) |
| GitHub Actions workflow to validate HTML on every push | Done — `.github/workflows/validate.yml` runs `html-validate` on every push/PR |
| All external links not broken | Verified where the sandbox network policy allows: the two project links (`github.com/25-THEBEaST-25/secure-auth-monitor`, `/login-guard`) return HTTP 200, and the actual Google Fonts stylesheet URL used by the page returns 200. LinkedIn, Instagram, and the site's own GitHub Pages URL could not be checked directly (this environment's egress proxy blocks those hosts) — all three are simple, standard-format profile/self URLs, but a full check needs to happen from an unrestricted network. |
| `resume.pdf` linked if it exists | Done — added a "Resume" button to the contact section (`index.html`), linking to the existing `resume.pdf` |

## Verification performed

- Ran `npx html-validate "**/*.html"` locally after the change — 0 errors.
- Confirmed via the GitHub API that the real "Validate HTML" CI run on `main` (commit `32adc96`) passed.
- Spot-checked external URLs with `curl`; two of the linked GitHub repos returned 200, and the Google Fonts stylesheet URL used by the page returned 200.

## Remaining caveat

LinkedIn, Instagram, and the GitHub Pages self-link should be spot-checked from a network that isn't proxy-restricted, since this session's sandbox couldn't reach those hosts to confirm a 200 directly.
