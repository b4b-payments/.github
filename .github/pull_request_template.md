<!--
  Change Management - Pull Request Template (v2.1)
  Source: Release Management - PCI DSS v4.0.1 Implementation Pack
  Canonical copy maintained in this release-notes tooling repo at
  .github/pull_request_template.md. The bootstrap script copies it into each
  product repo at the same path (a private org .github repo cannot serve it as
  an org-wide default).

  The developer does the thinking once. The release-notes and Tier 2/3 CR
  automation read from this PR (body + commits + diff + linked Jira ticket).
  Do not delete the section headers or the classification markers below -
  the automation parses them. Several sections are wrapped in collapsible
  <details> blocks for readability; keep the heading line (starting with two
  hash characters) inside each block, as the automation anchors on those
  headings (for example the PCI Impact Check heading).

  Comment `/release-notes-help` on any PR to get some further information on
  the process.
-->

## Classification

<!--
  REQUIRED: Tick EXACTLY ONE tier marker below. PRs cannot merge without a
  declared tier. The automation reads these markers:
  - Tier 3: emergency/hotfix change. ANY change delivered as a hotfix straight
    to a deployment branch (e.g. production) is Tier 3, regardless of whether
    it would otherwise be Tier 1 or Tier 2. No Jira CR is created
    automatically; the PR is not blocked on CR approval - use /hotfix-approve
    for emergency sign-off (file one on demand with /create-cr if needed).
    After deploying, back-merge the hotfix into every other branch
    (staging, main, sandbox, ...) via a PR per branch, running /back-merge on
    each.
  - Tier 2: a standalone Jira Change Request will be created automatically from
    this PR and the merge will be blocked until that CR reaches Approved.
  - Tier 1: no PCI-scoped control is affected; the change ships in the standard
    release bundle. No standalone CR is required.
-->

- [ ] **TIER 1** - No PCI Impact Check boxes are ticked. I confirm this change does not affect any PCI-scoped security control.
- [ ] **TIER 2** - One or more PCI Impact Check boxes below are ticked. A standalone Jira CR will be created automatically from this PR and linked here; this PR is blocked from merging until that CR is Approved.
- [ ] **TIER 3** - Emergency/hotfix change. ANY change delivered as a hotfix (straight to a deployment branch such as production) is Tier 3, whatever its PCI impact. No Jira CR is created automatically; merge is unblocked via `/hotfix-approve` (not CR approval), and a CR can be filed for audit on demand with `/create-cr`. After deploying, back-merge into the other branches via a PR per branch (`/back-merge`).

## Related Tickets

<!-- Jira ticket(s) this PR addresses, e.g. CARDZ-1234. -->

## Testing

<!-- Describe how this change has been tested. For Tier 2 changes the formal post-deployment verification steps belong in the Jira CR. -->

<details>
<summary><strong>Risk Assessment</strong> (expand)</summary>

## Risk Assessment

<!-- Required for all changes. Complete before the release management meeting reviews this PR. -->

**Risk rating** (tick one):

- [ ] Low - Well understood, tested, failure unlikely or easily contained
- [ ] Medium - Some uncertainty, moderate potential impact
- [ ] High - Significant uncertainty, broad or client-facing potential impact

**Impact assessment** (tick all that apply):

- [ ] Schema or data migration
- [ ] Authentication or authorisation
- [ ] Payment, card, or PII data path
- [ ] External API contract (external payment providers, partners)
- [ ] Spans multiple services or repos
- [ ] High-traffic or client-facing path
- [ ] None of the above

**Urgency** (tick one):

- [ ] Standard - can wait for the normal release window
- [ ] Deadline - business deadline within 48h
- [ ] Security or operational imperative - incident or security driven

> Urgency never reduces risk. A High risk change with a deadline is still a High risk change.

</details>

<details>
<summary><strong>PCI Impact Check</strong> (expand)</summary>

## PCI Impact Check

**Virtual card reveal**

- [ ] Touches the virtual card reveal API, endpoint, or service
- [ ] Changes how PAN/CV2 is fetched from external payment provider
- [ ] Changes how card details are returned to the mobile app or portal
- [ ] Affects how PAN or CV2 is rendered, how long it stays visible, or whether it can be copied

**Physical card PIN**

- [ ] Touches the PIN reveal, PIN set, or PIN change endpoint or service
- [ ] Changes how PIN requests are made to external payment provider
- [ ] Touches PIN block handling or cryptographic key handling
- [ ] Could cause PIN to appear in a log, error message, or stack trace

**External Payment Provider API (any endpoint)**

- [ ] Changes how the application authenticates to the external payment provider
- [ ] Changes shared HTTP client behaviour affecting security
- [ ] Changes how external payment provider API credentials are stored or rotated

**Authentication**

- [ ] Affects authentication service configuration (password policies, MFA, token expiry, session duration)
- [ ] Changes authentication service token validation (JWT verification, claims, token refresh)
- [ ] Modifies login, logout, or session management for any user type
- [ ] Changes MFA or SCA flows
- [ ] Changes failed authentication handling (lockout, rate limiting, errors)
- [ ] Affects OAuth flows (redirect URIs, PKCE, token handling)

**Authorisation and roles**

- [ ] Adds, removes, or changes a role, permission, or entitlement
- [ ] Changes what a cardholder or company admin can access or do
- [ ] Modifies API-level authorisation checks on any in-scope endpoint

**User to cardholder to card mapping (highest sensitivity)**

- [ ] Touches the mapping between an authentication service user and a cardholder record
- [ ] Modifies how a cardholder record maps to card record(s)
- [ ] Changes any lookup, query, join, or resolution in the user to card chain
- [ ] Affects validation that a user is authorised to act on a specific card
- [ ] Changes company/employer to cardholder relationship logic

**Web application security controls**

- [ ] Adds, removes, or changes a security header value (CSP, HSTS, X-Frame-Options, etc.)
- [ ] Changes a session cookie attribute (HttpOnly, Secure, SameSite, Domain, Path, expiry)
- [ ] Changes where or how authentication service tokens are stored client-side
- [ ] Adds, removes, or changes CSRF protection on any endpoint
- [ ] Changes CORS, rate limiting, or SRI on a public-facing endpoint

**Additional security controls**

- [ ] Changes what actions are audit logged, or could stop security events being logged
- [ ] Changes how sensitive fields are masked, truncated, or omitted
- [ ] Changes a business logic gate on a sensitive operation
- [ ] Changes secrets handling or egress config for an in-scope service
- [ ] Upgrades a security-relevant library or changes a base image for an in-scope service

</details>

