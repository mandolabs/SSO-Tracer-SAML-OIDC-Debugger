# Privacy Policy — SSO Tracer: SAML & OIDC Debugger

## Summary
SSO Tracer is a local troubleshooting tool for Single Sign-On (SSO). It does **not** sell, share, or transmit your data to any external service.

## What data the extension accesses
To help diagnose SSO login failures, the extension may access:
- **Network request metadata** related to authentication flows (e.g., URLs involved in SSO redirects, HTTP status codes, and selected headers).
- **SAML parameters** (SAMLRequest/SAMLResponse) and **OIDC/OAuth parameters** (authorize/callback query parameters such as `error`).
- **Visible page text** on common IdP/login error pages to extract error codes (e.g., AADSTS / MSIS / Okta codes).

## Redaction / masking
- Sensitive values such as cookies, authorization headers, tokens, and large encoded blobs are **masked by default** in the UI.
- The “Support snippet” feature produces **redacted** output intended for sharing with support teams.

## What data is stored
- Data is stored **locally in the browser** only (in-memory during use, and local settings like profiles/toggles).
- Users can **clear** traces at any time.

## What data is sent to third parties
- **None.** The extension does not send telemetry, analytics, or trace contents to any server.

## Contact
For support or privacy questions, please open an issue:
https://github.com/mandolabs/SSO-Tracer-SAML-OIDC-Debugger/issues
