# External Validation Report — AP Recovery Intelligence Evidence Room v3.1

Date: 2026-10-02

## Status
**PASS WITH HARDENING APPLIED**

This review cross-checks the sample against public third-party guidance and mature recovery-audit practices. It is not a certification, legal opinion, SOC report, accounting opinion, or endorsement by any cited organization.

## 1. AP recovery methodology — PASS
Public recovery-audit guidance from PRGX describes duplicate payments, overpayments, missed/unapplied credits, transaction analysis, exception queues, and the need to balance duplicate-detection criteria against false positives. The Evidence Room's use of:
- deterministic exception candidates,
- visible source records,
- explicit counterevidence,
- human verification,
- false-positive controls,
- root-cause hypotheses,
is consistent with those public practices.

**Hardening added:** credit-related findings are now explicitly transaction-level signals until confirmed through the vendor ledger, later periods, or supplier statements where necessary.

Sources:
- PRGX, "Accounts Payable Recovery Audit" / false-positive and exception-queue guidance.
- PRGX, "The Ultimate Guide to AP Recovery Audits."
- PRGX, modern recovery audit guidance (2026).

## 2. Economic-claim discipline — PASS
The sample keeps:
IDENTIFIED != CONFIRMED != RECOVERED

This is materially more conservative than typical marketing language. Synthetic identified exposure is not described as money saved, owed, found, or recovered.

## 3. Security and privacy posture — PASS WITH GATE
NIST CSF 2.0 is a voluntary risk-management framework, not a certification. The project's wording must remain "NIST CSF 2.0-informed" and must never imply certification or independent attestation.

NIST privacy guidance supports data minimization: only information directly relevant and necessary to the purpose should be collected/processed.

The California CCPA regulations effective January 1, 2026 include written-contract and purpose-limitation requirements for service-provider/contractor handling of personal information where those rules apply.

**Hardening added:** real production data is blocked until written handling terms define purpose, minimum fields, retention/deletion, access boundaries, and material subprocessors/transfer paths.

## 4. Web accessibility — PASS WITH HARDENING
WCAG 2.2 emphasizes keyboard-visible focus and avoiding obscured focus.

**Hardening added:**
- Skip-to-content link.
- Explicit `:focus-visible` indicators.
- Filter result count announced through an ARIA live region.
- Native buttons/details remain keyboard-operable.

A browser-based WCAG conformance audit should still be run on the final public URL before claiming any WCAG conformance level.

## 5. Outreach compliance — ACTION REQUIRED BEFORE SEND
FTC CAN-SPAM guidance states that commercial email must use accurate headers/subjects, clearly identify the message as an advertisement, include a valid physical postal address, provide a clear opt-out mechanism, and honor opt-outs.

The current draft structure already has a postal address and reply-based opt-out. Before first send, the body should also clearly disclose that it is a commercial message/advertisement.

## 6. Remaining non-blocking limitations
- No real-world precision/recall can be claimed until a permissioned real-data evaluation exists.
- No SOC 2 / ISO 27001 / independent attestation should be claimed.
- No customer logos, testimonials or recovery statistics should be displayed until real and permissioned.
- A final public-URL scan should include browser accessibility, TLS/headers, mobile rendering and broken-link checks.

## External sources used
- PRGX public AP recovery audit guidance and product materials.
- NIST CSF 2.0 Small Business Quick-Start Guide.
- NIST Privacy Framework / minimization guidance.
- California Privacy Protection Agency, CCPA regulations effective 2026-01-01.
- W3C WCAG 2.2.
- U.S. Federal Trade Commission CAN-SPAM compliance guidance.
