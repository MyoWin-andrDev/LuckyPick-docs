#  Development, Testing & Launch Plan

Document 11 outlines the final verification checklist, testing protocol, and handover requirements for launching LuckyPick EuroMillions on the Apple App Store and Google Play Store.

---

##  1. Testing Requirements

* **Algorithm Unit Testing:** Verify random entropy and constraint compliance (5 main numbers between 1–50; 2 lucky stars between 1–12; no duplicate numbers in a single line).
* **Ticket Checker Testing:** Verify ticket match calculation against all **13 prize tiers** using synthetic historical draw data.
* **Scraper Dry-Run Test:** Perform live automation tests during at least two consecutive Tuesday and Friday draws before public release.
* **In-App Purchase Sandbox:** Verify StoreKit 2 and Google Play Billing sandbox purchasing, renewal, and entitlement restoration.

---

##  2. Store Submission Checklist

- [x] App Icon & Assets (Gold & Dark Blue branding)
- [x] App Store & Google Play Screenshots
- [x] Privacy Policy & Terms of Service published at `https://luckypick.eu/privacy`
- [x] APNs & FCM Push Certificates uploaded
- [x] TestFlight & Google Play Beta testing completed
- [x] 100% Ad-Free compliance confirmed

---

##  Building & Previewing Documentation Locally

You can preview and build this documentation site using MkDocs:

```bash
# Preview documentation locally
cd /Users/myowin/LuckyPick
mkdocs serve

# Build static HTML production output
mkdocs build
```
