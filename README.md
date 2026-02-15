# SSO Tracer: SAML & OIDC Debugger

A browser extension to **trace, decode, and troubleshoot SSO login failures** across **SAML** and **OIDC/OAuth** flows.  
Built **Firefox-first**, with a Chromium MV3 variant.

> Redaction is **ON by default**. No telemetry/analytics.

---

## Features

- **Trace SSO network flows** (SAMLRequest/SAMLResponse, OIDC authorize/callback errors)
- **Decode and summarize** key data points:
  - SAML: issuer, status, audience, InResponseTo, NotOnOrAfter, signature presence
  - OIDC: client_id, redirect_uri, state, nonce, error / error_description
- Groups traffic into distinct **SSO Attempts** (Attempt #1, #2…) with per-attempt summary
- Highlights common failure causes:
  - redirect URI mismatch, consent required, MFA/CA required
  - audience/issuer mismatch, time skew / expired assertions
  - cookie/session issues (SameSite/third-party storage), redirect loops
- One-click **Shareable Support Snippet** (Text or Markdown), **redacted**
- Built-in **IdP Profiles** (Entra/Azure AD, Okta, Keycloak, ADFS, Ping, OneLogin) + editable JSON profiles

---

## Screenshots (optional)

Add images to `docs/` and update these links:

- Attempts + Diagnosis view  
  `docs/screenshot-attempts.png`

- Timeline + decoded detail  
  `docs/screenshot-timeline.png`

- Support snippet output  
  `docs/screenshot-snippet.png`

---

## Installation

### Firefox (temporary install for testing)
1. Download the latest ZIP from Releases (or build locally).
2. Go to `about:debugging#/runtime/this-firefox`
3. Click **Load Temporary Add-on…**
4. Select `manifest.json`

### Chrome / Edge (developer mode)
1. Unzip the Chromium build.
2. Go to `chrome://extensions`
3. Enable **Developer mode**
4. Click **Load unpacked**
5. Select the extension folder

---

## How to use

1. Open a new tab and start the login flow you want to troubleshoot.
2. Click the extension icon to open the popup.
3. Watch:
   - **Attempts**: grouped SSO tries (click one to filter)
   - **Diagnosis**: top findings for the selected attempt
   - **Timeline**: raw captured events
4. Click an event to see the **decoded detail**.
5. Use:
   - **Copy Snippet** / **Copy Snippet (MD)** to share a redacted report
   - **Export** to copy a full JSON bundle (report + snippet + attempts + trace)

**Tip:** If troubleshooting cookie/state issues, reproduce in:
- a **Private Window**, or
- a fresh profile, or
- with third-party cookie settings adjusted (for diagnosis only)

---

## Permissions rationale (AMO-friendly)

This extension requests broad permissions because SSO flows commonly involve **multiple domains** (service provider + IdP).

- `<all_urls>`  
  Needed to observe redirects across IdP/SP domains (e.g., login.microsoftonline.com, okta.com, /realms/…).
- `webRequest`  
  Needed to read request URLs and relevant response headers during authentication flows.
- `tabs`  
  Used to associate traces with the active tab and show tab context in the UI.
- `storage`  
  Stores local settings (UI toggles) and profile configuration. No cloud sync required.

No permissions are used to block or modify traffic.

---

## Privacy

- **No telemetry / analytics.**
- Traces remain **local to the browser** and are only exported when the user clicks Export or Copy Snippet.
- Sensitive values (cookies, auth headers, tokens, SAML payloads, large blobs) are **masked by default**.

See full policy: **PRIVACY.md**  
https://github.com/mandolabs/SSO-Tracer-SAML-OIDC-Debugger/blob/main/PRIVACY.md

---

## Limitations / Notes

- Some IdPs use POSTed forms for SAML responses; the extension decodes SAML where possible, but browser APIs may limit access to certain POST bodies.
- Encrypted SAML assertions cannot be decoded without keys (the extension will still show metadata).
- This tool is intended for **debugging and support**, not for credential capture.

---

## Troubleshooting

If the timeline looks empty:
- Ensure the login flow happens in the **same tab** you’re inspecting
- Try reproducing the issue again and reopen the popup
- Confirm the extension is enabled and has required permissions

If you suspect cookie/state problems:
- Try a Private Window
- Check third-party cookie settings and storage partitioning
- Look for “Redirect loop detected” or “No Set-Cookie observed” in Diagnosis

---

## Contributing

PRs welcome:
- Add new IdP mappings (error codes → hints)
- Improve flow grouping heuristics
- Add additional decoders / vendor profiles

---

## License

Choose a license and add `LICENSE` (MIT recommended for simplicity).
