# NPP Storm Inspection Form and CRM Integration

**Draft technical requirements and launch checklist**  
**Prepared:** November 15, 2026  
**Status:** Requirements draft; production launch is blocked until the form-to-CRM path and consent review pass end-to-end testing.

## Current-state finding

The supplied storm-damage landing page states that its form is a visual demonstration, is not connected to NPP’s GoHighLevel CRM, and does not transmit or store submissions. It also says CRM integration and consent/privacy review are required before paid advertising. Treat this as a **NO-GO for paid traffic** until production behavior is implemented and verified.

## Proposed user experience and fields

Keep the existing request focused on a storm or roofing concern. The page currently shows first name, last name, phone, email, property ZIP, request type, and optional additional details.

Recommended minimum required fields are first name, last name, one valid contact method (phone or email), property ZIP, and request type. Keep additional details optional. Confirm with NPP whether both phone and email are operationally necessary before making both mandatory. Normalize phone numbers server-side and validate ZIP codes without rejecting valid ZIP+4 formats. Confirm service-area behavior for ZIP codes outside Maryland, Washington, D.C., and Northern Virginia.

Display a clear privacy notice and purpose-specific consent controls. Separate consent for requested follow-up from optional promotional email/text marketing. Do not pre-check optional marketing consent. Store the consent choice, timestamp, and the language/version shown with the lead. NPP and qualified counsel should approve the exact disclosure text and applicable call/text rules before release.

## Integration and data requirements

1. **Submission path:** Send form data to a server-side endpoint or an approved, secured GoHighLevel integration. Do not expose a private CRM API key in client-side JavaScript. Use HTTPS and separate staging and production credentials.
2. **CRM target:** Confirm the correct GoHighLevel account/location, contact fields, pipeline/stage (if used), lead owner, notification recipients, and follow-up process with NPP before configuration.
3. **Field mapping:** Map first name, last name, phone, email, property ZIP, request type, additional details, source page, campaign/ad identifiers, UTMs, and consent state to approved CRM fields. Store submission timestamp and consent-text version. Do not place personal information in URLs or analytics parameters.
4. **Duplicate control:** Use an idempotency key or equivalent request identifier to avoid duplicate lead creation on repeat clicks or network retries. Agree on how matching email/phone contacts are updated or flagged; do not overwrite valuable existing contact data without a rule.
5. **Reliability:** Report success to the page only after the server accepts the lead and the CRM integration confirms acceptance. Retry transient failures safely and alert an assigned owner if retries fail. Show a plain-language error and NPP’s approved phone fallback rather than a false success message.
6. **Spam and abuse controls:** Validate on both client and server. Add rate limiting and a honeypot or risk-based challenge as appropriate. Keep error messages useful without revealing system internals.
7. **Privacy and security:** Restrict API access to the required CRM location and permissions, store secrets outside client code, limit PII in logs and internal notifications, define access and retention, and document deletion/correction handling. NPP and counsel must approve privacy and consent obligations for the jurisdictions served.
8. **Notifications and follow-up:** Specify who receives new-lead alerts, which CRM status/tag is applied, business-hour expectations, and who owns each follow-up. Do not promise a response time in the page or ads until NPP approves and can meet it.
9. **Attribution and analytics:** Persist approved UTMs and ad/click identifiers to CRM fields. Fire a lead event only after a valid accepted submission. If Meta Pixel and server-side Conversions API are used, make events consent-aware and deduplicate using a shared event ID. Do not send PII in URLs or event labels.

## Acceptance criteria

The work is ready for release only when all of these are true:

- A valid test submission appears exactly once in the correct GoHighLevel location with correct contact details, request type, ZIP, attribution, consent record, timestamp, status/tag, and owner.
- Missing or invalid fields produce accessible, understandable errors and do not create a CRM record.
- Duplicate clicks and safe retries do not create duplicate records.
- Simulated network/CRM failures do not show success; the visitor sees a recoverable message and the assigned owner receives an alert after retry exhaustion.
- Success confirmation and internal notifications match NPP’s approved follow-up process.
- Analytics count an accepted lead once, do not count failed/abandoned attempts, and do not expose personal data.
- Consent language, privacy notice, tracking behavior, retention, and marketing permissions have NPP/counsel sign-off.
- Mobile and desktop QA passes in current major browsers; keyboard operation, field labels, focus order, contrast, and error announcements are checked.
- Test data is removed, production secrets are set, and a final smoke test is recorded.

## Launch checklist

### Product and business decisions
- [ ] Confirm required fields and whether phone, email, or either may be supplied.
- [ ] Confirm service-area ZIP handling and out-of-area response.
- [ ] Confirm GoHighLevel account/location, field names, pipeline/stage (if used), tags, owner, and internal notification route.
- [ ] Confirm visitor success/error text, phone fallback, and follow-up expectation.
- [ ] Approve privacy notice, consent language, contact channel permissions, retention, and cookie/analytics behavior.

### Implementation
- [ ] Connect the form to a secured server-side integration; keep CRM credentials out of the browser.
- [ ] Implement server-side validation, idempotency, duplicate rules, spam mitigation, safe retries, and failure alerting.
- [ ] Map source URL and approved campaign/UTM fields into the CRM.
- [ ] Add consent-aware, success-only analytics events; deduplicate client/server events if both are used.
- [ ] Confirm HTTPS, access controls, secret handling, and PII-safe logs.

### QA and release
- [ ] Test valid, invalid, missing, out-of-area, duplicate, spam, and failed-network submissions.
- [ ] Confirm a valid submission creates one CRM record with correct attribution and consent evidence.
- [ ] Confirm no record or conversion event is created for invalid/failed submissions.
- [ ] Test mobile, desktop, keyboard navigation, field errors, confirmation, and fallback contact route.
- [ ] Verify CRM notifications and assign a real follow-up owner.
- [ ] Remove test leads and record sign-off from engineering, NPP marketing/operations, and the privacy reviewer.
- [ ] Only then update campaign ads to point at this production URL and enable paid traffic.

## Open decisions / owners

- GoHighLevel account/location and credential owner: **[NPP to assign]**
- Required fields and duplicate policy: **[NPP to approve]**
- Lead owner, notification channel, and follow-up standard: **[NPP to assign]**
- Consent/privacy text and tracking review: **[NPP and qualified counsel]**
- Analytics stack and event IDs: **[Marketing/engineering to confirm]**
- Production URL and go-live approval: **[NPP to approve after QA]**

## Reference pages

- [NPP storm-damage landing page](https://summit-leads-website-portfolio.vercel.app/npp/storm-damage/)
- [NPP official storm-inspection page](https://www.newparadigmprojects.com/storm-inspection)
