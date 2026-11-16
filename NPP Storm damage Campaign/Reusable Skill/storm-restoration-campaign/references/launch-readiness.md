# Lead-path and campaign readiness

Use this checklist when paid social traffic will lead to a landing-page form, CRM, or conversion event. Mark each item **Pass**, **Fail**, or **Not applicable**, and name an owner for each failure. A failed form-to-CRM or consent check is a launch blocker.

## Destination and form

- [ ] Production URL is final, loads over HTTPS, works on common mobile and desktop browsers, and matches the ad’s offer and service area.
- [ ] All fields have labels, clear required/optional state, appropriate input types, and accessible inline validation.
- [ ] Required fields are minimal. A reasonable default is name, one usable contact method, service ZIP/postal code, and request type; confirm the business’s follow-up needs before enforcing both phone and email.
- [ ] Service-area behavior, success message, and a clear fallback phone/contact path are defined.
- [ ] Consent controls are clear, purpose-specific, unchecked by default where opt-in applies, and linked to the current privacy notice. Legal review covers the applicable call/text/email permissions and jurisdictions.
- [ ] No form copy promises a response time, inspection result, insurance outcome, or offer condition that the business has not approved.

## Secure delivery to CRM

- [ ] Browser submission reaches a server-side endpoint or an approved, secured native CRM integration. No private CRM API key is exposed in browser code.
- [ ] CRM location/account, field mapping, source, campaign, asset/ad identifiers, consent state, consent copy/version, and timestamp are agreed and tested.
- [ ] Duplicate handling and idempotency prevent double-clicks/retries from creating duplicate leads.
- [ ] Transient CRM failures retry safely and alert the assigned owner; the visitor is not shown a false success state.
- [ ] Spam controls are proportionate (validation, rate limits, honeypot, or risk-triggered challenge). Avoid collecting unnecessary sensitive data.
- [ ] Logs and notifications avoid unnecessary personal information; credentials use secrets management, least privilege, and a rotation plan.
- [ ] Lead ownership, notification route, CRM status/pipeline, and follow-up responsibility are tested with the business.

## Analytics and privacy

- [ ] UTM and approved click identifiers are captured and mapped without putting personal data in URLs.
- [ ] A lead/conversion event fires only after the form is accepted by the server/CRM, not on button click or validation failure.
- [ ] Pixel/server events, if used, are consent-aware and deduplicated; no personal data is sent in event names or query strings.
- [ ] Privacy notice, cookie/analytics behavior, access, retention, and deletion process are reviewed by the responsible business owner and qualified counsel.

## End-to-end QA

- [ ] Test valid lead appears once in the correct CRM location with correct fields, attribution, consent record, status, and owner.
- [ ] Test invalid, missing, out-of-area, spam, duplicate, and repeat-click submissions.
- [ ] Simulate network timeout/CRM failure and verify retry, alert, and user-facing error/fallback.
- [ ] Verify confirmation message, email/SMS notifications, and routing using test data—not a real consumer’s information.
- [ ] Verify analytics counts one accepted lead and zero for failed/abandoned submissions.
- [ ] Remove test data, confirm production credentials/configuration, run one final smoke test, and record sign-off.

## Campaign release gate

- [ ] Final creative and captions use the official logo and only approved factual claims.
- [ ] CTA destination matches the tested production form or approved alternative.
- [ ] Platform preview, placement crop, safe areas, captions, audio, links, and tracking parameters are checked.
- [ ] A named campaign owner approves creative, destination, tracking, budget, and schedule before activation.
