# Twilio A2P Campaign Compliance Report
Generated: 2026-03-20

## Overall Status: ⚠️ NEEDS FIXES

The opt-in form language and structure are strong and address the core rejection reason (Error 30513). Two issues remain: (1) the server-side doesn't record the consent timestamp to the DB, creating a TCPA audit-trail gap; and (2) the opt-in URL submitted to Twilio must be a real, inspectable URL — reviewers can't use a 404'd token link. Fix both before resubmitting.

---

## Checklist Results

| # | Requirement | Status | Notes |
|---|-------------|--------|-------|
| 1 | Explicit opt-in checkbox (not passive text) | ✅ PASS | `<input type="checkbox" id="sms_consent" required>` present |
| 2 | Checkbox unchecked by default | ✅ PASS | No `checked` attribute — unchecked by default |
| 3 | Consent language says "text messages" explicitly | ✅ PASS | "I expressly consent to receive **text messages** from Gleam" |
| 4 | Consent language names the company | ✅ PASS | "from Gleam (a LucraLab product)" |
| 5 | Consent language describes message types | ✅ PASS | "Google review alerts, suggested reply drafts for my approval, and account notifications" |
| 6 | Message frequency disclosure | ✅ PASS | "Message frequency varies" |
| 7 | "Message & data rates may apply" | ✅ PASS | Present verbatim in checkbox label |
| 8 | STOP instructions | ✅ PASS | "Reply STOP to unsubscribe at any time" |
| 9 | Marketing consent is SEPARATE from service consent | ✅ PASS | Two separate checkboxes, visually distinct |
| 10 | Marketing consent is OPTIONAL (not required to submit) | ✅ PASS | No `required` attribute; labeled "(Optional)"; submit button only gated on service checkbox |
| 11 | Marketing checkbox unchecked by default | ✅ PASS | No `checked` attribute |
| 12 | Privacy Policy live and publicly accessible | ✅ PASS | gleamreply.com/privacy.html → HTTP 200; /privacy → HTTP 200 |
| 13 | Terms of Service live and publicly accessible | ✅ PASS | gleamreply.com/terms.html → HTTP 200; /terms → HTTP 200 |
| 14 | PP mentions SMS/text messaging and phone number use | ✅ PASS | Section 2 ("Mobile phone number") and Section 3 (Twilio SMS) explicitly cover this |
| 15 | ToS mentions SMS and consent | ✅ PASS | Dedicated Section 2 "SMS Communications & Consent" with STOP, TCPA, frequency, and rates |
| 16 | PP and ToS linked from the opt-in form | ✅ PASS | Linked within the consent checkbox label AND in the form footer legal-links block |
| 17 | Opt-in form is publicly accessible or submittable URL | ⚠️ PARTIAL | Form exists at `/setup/{token}` but token-gated — Twilio reviewers need a valid demo URL |
| 18 | Server records SMS consent timestamp | ❌ FAIL | `sms_consent_at` column exists in `Practice` model but `setup_post()` never writes to it |

---

## Issues Found

### Issue 1 — CRITICAL: Server-side consent timestamp not recorded
**Problem:** The `Practice` model has `sms_consent_at: Mapped[datetime | None]` for TCPA compliance, but `setup_post()` in `routers/onboarding.py` never writes to it. If Twilio or a regulator ever audits, you have no server-side record of when consent was given.

**Fix (code change):** In `setup_post()` in `/home/ubuntu/src/reviewflow/routers/onboarding.py`, add consent capture after the phone validation block:

```python
# Capture form fields
sms_consent_val = (await request.form()).get("sms_consent")
marketing_consent_val = (await request.form()).get("marketing_consent")

# ... existing phone / GBP validation ...

practice.manager_phone = cleaned
practice.business_type = business_type or "Local Business"
practice.google_location_name = location_name
practice.active = True
practice.sms_consent_at = datetime.utcnow()   # ← ADD THIS
# Optionally: practice.marketing_consent = bool(marketing_consent_val)
```

Or more cleanly, add `sms_consent: str = Form(default=None)` and `marketing_consent: str = Form(default=None)` as named Form parameters so FastAPI extracts them automatically.

### Issue 2 — IMPORTANT: Twilio opt-in URL must be an inspectable, working page
**Problem:** The opt-in form lives at `https://api.gleamreply.com/setup/{token}` — tokens are unique per customer and expire. When Twilio reviewers visit the URL submitted in the campaign, they'll get a 404. Twilio requires a URL where they can actually see the opt-in experience.

**Fix (two options):**
- **Option A (recommended):** Create a static demo page at `https://gleamreply.com/sms-opt-in` or similar that mirrors the consent form UI (can be non-functional/display-only) and shows both checkboxes with the full consent language. Submit that URL to Twilio.
- **Option B:** Keep a long-lived test/demo token active in the DB specifically for Twilio review purposes. Set `created_at` far in the future to prevent expiry. Submit `https://api.gleamreply.com/setup/{demo-token}` to Twilio.

### Issue 3 — MINOR: Footer links on index.html use paths without .html extension
**Problem:** `index.html` footer links to `/privacy` and `/terms`. These currently return HTTP 200 (the server resolves them), but they're inconsistent with the actual filenames `privacy.html` / `terms.html`. Not a Twilio blocker but worth standardizing.

**Fix:** Either update footer to `/privacy.html` and `/terms.html`, or keep as-is since both routes resolve.

### Issue 4 — MINOR: Marketing checkbox `onchange=""` is empty
**Problem:** The marketing checkbox has `onchange=""` — harmless but noise. Can be removed.

**Fix:** Change `onchange=""` to remove the attribute entirely: `<input type="checkbox" id="marketing_consent" name="marketing_consent">`.

---

## What's Already Good (Do Not Change)

The following items were correct and should NOT be altered before resubmission — these directly address the two previous rejection reasons:

- ✅ Two separate checkboxes (service vs. marketing) — addresses mixed use case rejection
- ✅ Service checkbox has `required` attribute, marketing does not
- ✅ Submit button starts `disabled`, re-enabled only when service consent is checked (`onchange="document.getElementById('submit-btn').disabled=!this.checked;"`)
- ✅ Consent language is explicit, complete, and properly formatted
- ✅ Both PP and ToS are linked inline within the consent text (not just in footer)
- ✅ Both PP and ToS have dedicated SMS sections
- ✅ Both `/privacy` and `/privacy.html` routes return 200

---

## Submission Checklist for James

When resubmitting in Twilio console, use these **exact** values:

### Opt-in URL
```
https://gleamreply.com/sms-opt-in
```
*(Create this static demo page first — see Issue 2 above. Do NOT submit the /setup/{token} URL.)*

### Privacy Policy URL
```
https://gleamreply.com/privacy.html
```

### Terms of Service URL
```
https://gleamreply.com/terms.html
```

### Message Flow Description (paste this verbatim)
```
Users opt in to receive SMS during web-based account setup at gleamreply.com. 
The onboarding form presents two separate consent checkboxes:

(1) SERVICE MESSAGES (required): An explicit, unchecked-by-default checkbox 
with the following language: "By checking this box, I expressly consent to 
receive text messages from Gleam (a LucraLab product) at the mobile number 
provided above. Messages will include Google review alerts, suggested reply 
drafts for my approval, and account notifications. Message frequency varies. 
Message & data rates may apply. Reply STOP to unsubscribe at any time." 
Links to Privacy Policy and Terms of Service are embedded in this consent text. 
The submit button is disabled until this checkbox is checked.

(2) MARKETING MESSAGES (optional): A separate, unchecked-by-default checkbox 
with the following language: "(Optional) I also agree to receive occasional 
marketing messages from Gleam, such as product updates, tips, and promotional 
offers. You can opt out at any time by replying STOP."

Users cannot submit the form without checking the service consent checkbox. 
The marketing checkbox is entirely optional and has no effect on form submission.
```

### Use Case
```
Mixed — Service (primary) + Marketing (optional, separate consent)
```

### Sample Messages

**Sample 1 (Review Alert — Service):**
```
Gleam | New 2-star review from John D: "Wait time was too long and staff seemed rushed." Here's a draft reply: "Thank you for your feedback, John. We're sorry your visit didn't meet expectations — we'd love the chance to make it right. Please reach out at [phone]." Reply APPROVE to post, EDIT [your text] to customize, or IGNORE to skip. Reply STOP to opt out.
```

**Sample 2 (Auto-post Confirmation — Service):**
```
Gleam | Auto-posted a response to a new 5-star review from Sarah M. "Thanks for the kind words, Sarah! We appreciate your support." Reply MENU for commands. Reply STOP to opt out.
```

**Sample 3 (Account Notification — Service):**
```
Gleam | Your weekly review summary: 3 new reviews (avg 4.3★). 2 auto-posted, 1 approved by you. Keep it up! Reply MENU for commands or STOP to opt out.
```

---

## Priority Order Before Resubmitting

1. 🔴 **Create the static opt-in demo page** at `gleamreply.com/sms-opt-in` (blocker — Twilio reviewer will be checking this URL)
2. 🔴 **Fix `setup_post()` to write `sms_consent_at = datetime.utcnow()`** (TCPA compliance — legal requirement)
3. 🟡 Remove the empty `onchange=""` from marketing checkbox (cosmetic)
4. 🟢 Resubmit with message flow description above pasted verbatim

The consent form language itself is solid and correctly structured. The rejections were about form/submission mechanics, not about the underlying language — which is now in good shape.
