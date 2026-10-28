# Intent: Results-ready notification

Sources: `01` = `inputs/01-approved-prd.md` (PRD N-17, approved 2026-09-18); `02` = `inputs/02-current-meeting.md` (discovery notes, 2026-09-20). `inputs/03-superseded-request.md` is excluded as a source of approval: `03`: "Status: SUPERSEDED by approved PRD N-17, 2026-09-18. This is historical context, not current approval."

## Problem

- **P-1** The fictional clinic receives avoidable calls from patients checking whether their results are ready.
  `01`: "The fictional clinic receives avoidable calls from patients checking whether results are ready."

## Proposed outcome

- **I-1** The patient is notified when a result is ready for their review in the existing authenticated portal.
  `01`: "Notify the patient when a result is ready for their review in the existing authenticated portal."
- **I-2** "Ready" means a doctor has reviewed and released the result, not that the laboratory upload finished.
  `01`: "A doctor must review and release the result before any notification is eligible." `02` (product owner): "'Ready' must not mean that the laboratory upload merely finished."
- **I-3** The notification only says that an update is available and directs the patient to the existing authenticated portal.
  `01`: "The notification says that an update is available and directs the patient to the existing authenticated portal."
- **I-4** In scope: the existing portal result route, preventing duplicate notifications, and handling delivery failures.
  `01`: "Use the existing portal result route." `01`: "Avoid duplicate notifications for the same released result version; handle delivery failures without duplicate patient messages."

### How success will be observed

- **S-1** A reduction in results-status calls is measured, counting status-only calls separately from clinical questions against a measured baseline.
  `01`: "Measure reduction in results-status calls and delivery failures." `02` (support lead): "count status-only calls separately from clinical questions; compare against a measured baseline."
- **S-2** Delivery failures are measured.
  `01`: "Measure reduction in results-status calls and delivery failures."
- **S-3** No baseline or numerical target is approved; both are agreed during discovery, so this intent sets no target.
  `01`: "The baseline and numerical target will be agreed during discovery; none is approved yet."

## Affected users and systems

- **U-1** Patients, who receive the notification. `01`: "Notify the patient when a result is ready for their review in the existing authenticated portal."
- **U-2** Doctors, who review and release results. `01`: "A doctor must review and release the result before any notification is eligible."
- **U-3** Clinic support, which counts the calls. `02` (support lead): "count status-only calls separately from clinical questions; compare against a measured baseline."
- **U-4** The existing authenticated portal and its result route. `01`: "Use the existing portal result route." `02` (engineering lead): "the existing portal path is adequate."
- **U-5** Notification messages and the notification and operational logs. `01`: "No diagnosis, test result, clinical measurement or treatment detail goes in the message or notification logs." `02` (privacy owner): "no sensitive content in messages or operational logs."
- **U-6** Decision owners: product owner, privacy owner, clinical owner, engineering lead and support lead, as named in `01` and `02`.

## Out of scope

- **X-1** Portal redesign, appointment scheduling, clinical interpretation and notifying third parties.
  `01`: "Portal redesign, appointment scheduling, clinical interpretation and notifying third parties are outside this approved scope."
- **X-2** A new patient dashboard.
  `02` (engineering lead): "A new patient dashboard is a separate project."
- **X-3** Referring-doctor notification is not approved here; it stays open as OPEN-2.
  `02` (clinical owner): "do not infer approval for referring-doctor notifications from the old request."
- **X-4** Anything proposed only in the superseded early request (`03`): notifying on lab upload, putting result content in a message, copying the referring doctor, rebuilding the dashboard, and its call-reduction target.
  `03`: "This is historical context, not current approval."

## Constraints

- **C-1** A doctor must review and release the result before any notification is eligible.
  `01`: "A doctor must review and release the result before any notification is eligible." `02` (product owner): "keep the PRD's review-before-notification gate."
- **C-2** No clinical or other sensitive content in the message or in notification and operational logs; the message carries only that an update is available.
  `01`: "No diagnosis, test result, clinical measurement or treatment detail goes in the message or notification logs." `02` (privacy owner): "no sensitive content in messages or operational logs."
- **C-3** Access is authenticated in the existing portal, with no attached results and no public result link.
  `01`: "Authenticate access in the existing portal. Do not attach results or introduce a public result link."
- **C-4** Avoid duplicate notifications for the same released result version.
  `01`: "Avoid duplicate notifications for the same released result version"
- **C-5** Handle delivery failures without duplicate patient messages.
  `01`: "handle delivery failures without duplicate patient messages."
- **C-6** Use the existing portal result route.
  `01`: "Use the existing portal result route." `02` (engineering lead): "the existing portal path is adequate."
- **C-7** Only the patient is an approved recipient; no other recipient is approved until its owners decide.
  `01`: "Notify the patient"; "It is not approved by this PRD." (referring doctor)

## Open questions with their owners

- **OPEN-1** Channel: SMS, email or portal push? Owners: **product owner and privacy owner**, after the consent and delivery review.
  `01`: "Channel (SMS, email, portal push): product owner and privacy owner must decide after consent/delivery review." `02` (privacy owner): "Consent and the actual channel are still under review."
- **OPEN-2** Should the referring doctor be notified, and is that recipient authorized? Owners: **clinical owner and privacy owner**.
  `01`: "Notification to the referring doctor: clinical owner and privacy owner must decide recipient authorization. It is not approved by this PRD." `02` (clinical owner): "do not infer approval for referring-doctor notifications from the old request."

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
