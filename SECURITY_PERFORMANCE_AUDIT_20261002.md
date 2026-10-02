# AP Recovery Intelligence — Security & Performance Audit v1

Date: 2026-10-02
Scope: public static site, GitHub source, and Render deployment configuration observable through connected tooling.

## Executive status
**HARDENED WITH ONE PRIVACY REMEDIATION AND ONE HEADER-LEVEL ITEM STILL OPEN**

## High-priority findings

### P1 — Historic physical-address exposure in public Git history
Status: OPEN / confirmed.
The current public page no longer displays the full street address, but an earlier public commit of index.html does. Replacing the current file does not erase Git history.

Recommended remediation:
1. Rewrite repository history with git-filter-repo or recreate the repository from a clean snapshot.
2. Force-push the cleaned history.
3. Review forks/clones.
4. If permanent cached-view removal is required, follow GitHub's sensitive-data-removal process.

Do not copy the historic address into future repository documentation.

### P1 — Scroll content intentionally hidden until viewport intersection
Status: FIXED in v3.4.
The reveal pattern used opacity:0 until JavaScript IntersectionObserver activation. This directly caused content to appear progressively while scrolling. All primary content now paints immediately.

### P1 — Expensive continuous compositing on mobile
Status: FIXED in v3.4.
Removed continuous pulse/float/halo/proof-chain animations, large blur filters and backdrop-filter dependency. Mobile now disables decorative ambient/halo/orb layers.

## Security findings

### S1 — Remote font dependency
Status: FIXED.
Google Fonts connections were removed. Typography now uses local system font stacks. This reduces render-blocking/network variability and removes an unnecessary third-party request.

### S2 — Client-side injection resilience
Status: HARDENED.
The Evidence Room still renders controlled synthetic data into HTML, but all dynamic string values are now HTML-escaped before insertion. Current data is trusted/static; this hardening protects future versions if the data source changes.

### S3 — Content Security Policy
Status: PARTIALLY FIXED.
A restrictive CSP meta policy is now present: self-only scripts/styles/images/fonts, no network connects, no objects, no forms and no frames.
For full clickjacking protection, HTTP response headers remain preferable because frame-ancestors cannot be enforced through a CSP meta tag.

### S4 — HTTP security headers
Status: OPEN at hosting layer.
Recommended Render response headers:
- Content-Security-Policy as an HTTP header
- X-Frame-Options: DENY
- X-Content-Type-Options: nosniff
- Referrer-Policy: no-referrer or strict-origin-when-cross-origin
- Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=()
- Strict-Transport-Security after verifying HTTPS/domain strategy

The connected Render API does not expose custom-header mutation for the existing site, so this requires Render Dashboard configuration or a Blueprint-managed service.

## Performance findings

### PERF1 — Render/CDN size is not the primary bottleneck
Observed bandwidth during the audit window was about 0.042 MB. HTTP latency/request data was not available in the metrics response because traffic is currently sparse.
Render provides HTTP/2, Brotli and CDN delivery for static sites.

### PERF2 — Web fonts
Status: FIXED.
Removed third-party font CSS and font downloads.

### PERF3 — Continuous effects
Status: FIXED.
Removed continuous JavaScript/CSS animation loops and 3D pointer tracking.

### PERF4 — GPU-heavy filters
Status: FIXED.
Removed backdrop-filter and expensive blur filters from core UI. Mobile receives an even lighter rendering path.

### PERF5 — Layout shift
Status: HARDENED.
Brand SVG dimensions are explicit in markup.

## Remaining limitations
- No true Lighthouse/WebPageTest run could be executed from the available browser environment because the public onrender subdomain is not reachable from that inspection tool.
- Therefore no fabricated Performance/LCP/INP/CLS scores are reported.
- A real-device Chrome Lighthouse run remains the best final quantitative check.

## Release target
v3.4 — performance/security hardening.