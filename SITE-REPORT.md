# Site refresh report (Oct 25, 2026)

Branch `site/oct-2026-refresh` in two repos. Nothing is merged or deployed.

- **cascadeheadache.com** (`urkovs/cascade-headache-site`): items 1 to 6.
- **embertracker.app** (`urkovs/embertracker-landing`): item 7. The "Add your clinic" page lives there (`providers/join/`), not in this repo, so it has its own PR.

Delete this file before merging. Netlify would serve it at `/SITE-REPORT.md`.

## Pages changed

| Page | Changes |
|---|---|
| `/` (home) | New title, meta and JSON-LD description. Utility bar and hero rewritten for boutique positioning. Ember section moved directly under the hero, with equal badges and an embertracker.app link. "Seen within 2 weeks" added to care options. Rescue injections removed. Discovery call removed from the closing band. Store trademark line in the footer. |
| `/services/` | New prices. Discovery call tier removed (grid now 3 cards). Rescue injections removed. Sliding-scale section removed. Meta descriptions updated. Lede and closing band rewritten. |
| `/botox/` | Price copy now reads $350 plus the cost of Botox. Discovery call removed from the closing band. |
| `/ember/` | Badges made equal height (44px on small phones, 52px elsewhere). Trademark line in footer. |
| `/resources/` | Badges made equal height. Discovery call removed from the closing band. Trademark line in footer. |
| `/contact/` | Discovery call removed from the closing band. |
| `/drurkov/` | "Book a discovery call" button now "Book an appointment". |
| `assets/site.css` | Shared `.store-badges` component. Tier grid set to 3 columns (1 column under 760px). |
| `sitemap.xml` | `lastmod` bumped on changed pages. |
| embertracker.app `/providers/join/` | Full rewrite (see item 7). Meta, `llms.txt` and sitemap updated to match. Form markup is byte-identical. |

## Before and after

**Home title**
- Before: Cascade Headache | Find Relief Today — Book Now
- After: Cascade Headache | Home of Ember and Boutique Migraine Care

**Home meta description**
- Before: Specialty migraine and headache care across Washington. Telemedicine visits with a headache specialist, plus in-person procedure days in Lacey, WA.
- After: Cascade Headache makes Ember, a free migraine tracker for iPhone and Android. We also offer boutique migraine care in Washington. Most new patients are seen within 2 weeks.

**Home hero**
- Before: Now accepting patients from Washington / Integrative Headache Care / A clinic built to serve patients with complex needs that other providers find challenging. Buttons: Book an appointment, Meet Dr. Urkov.
- After: Boutique migraine care in Washington / Integrative Headache Care / Personal migraine care from a headache specialist. Most new patients are seen within 2 weeks of first contact. Buttons: Request an appointment, Get the free Ember app.

**Home Ember section** (moved from the bottom of the page to directly under the hero)
- Before: Free for our patients and everyone else. App Store badge only. "Free on iPhone. Android version coming soon."
- After: Made by Cascade Headache. "Migraine tracking, without the headache. A few taps a day become patterns you can see and a report your clinician can use. Built by Dr. Urkov. Free on iPhone and Android." Both store badges plus "Visit embertracker.app".

**Prices**
| Visit | Before | After |
|---|---|---|
| Discovery call | $30 | Removed |
| Initial visit | $300 | $450 |
| Follow-up | $180 | $250 |
| Botox injection visit | $350 (medication billed separately at our cost) | $350 plus the cost of Botox |

**Closing bands** (home, services, botox, contact, resources)
- Before: Book a visit, or start with a discovery call to see if we're a good fit.
- After: Request an appointment. Most new patients are seen within 2 weeks.

**Sliding scale** (services, Payment)
- Before: "Making Care Accessible" with a sliding scale based on financial need and an invitation to reach out about cost.
- After: Removed. Payment keeps the cash-pay, FSA/HSA and superbill paragraphs.

**Store badges**
- Before: Google Play rendered visibly smaller. Its PNG carries transparent padding (168px badge inside a 250px image), so at the same box height the visible badge was about two thirds the App Store badge.
- After: Both badges render at the same visible height on every page (measured in Chromium: 48/48 on home and resources, 52/52 on /ember/, 44/44 on /ember/ under 400px). Gap is at least a quarter of the badge height for clear space. Apple and Google trademark attribution added to the footer on badge pages. This uses the same crop technique embertracker.app already uses. Official badge images only.

**Item 7: Add your clinic to Direct Send** (embertracker.app)
- Before: H1 "Add your clinic to Ember". One lead line ("Patients send their Ember report to your clinic's secure inbox from their own phones. It's free for your clinic and your patients.") and three "once confirmed" steps beside the form.
- After, in order:
  1. Hero: "Add your clinic to Direct Send." Patients email their Ember report from their own phone; Ember supplies the clinic address.
  2. How it works: sending is email from the patient's own account; the report doesn't pass through Ember's servers.
  3. What arrives: one email with one PDF. Subject names the patient and date. PDF is a short summary and chart note, then the B&W calendar for up to 90 days. Name only, no date of birth. No EHR connection.
  4. Patient control: the patient reviews first and nothing leaves the phone until they tap Send.
  5. Setup: four steps (request, confirm inbox and test report, clinic added by name, QR code and AVS link). Inbox guidance. Cost: free.
  6. One form, the only call to action. The hero's "Go to the setup form" link jumps to it.
- Sources: `ember-app/.claude/rules/clinic-packet.md` (packet contract, transport rules), embertracker.app `/providers/` FAQ and `/privacy/`. I left the gated Plus relay out because it isn't public.

## Open TODOs

Updated Oct 25 after Sam's answers.

1. **Good Faith Estimate.** Still open. No GFE notice exists on the site. See the note in the conversation; waiting on a decision.
2. ~~Setup timing~~ Done. The page now says "usually the same day, and always within 5 business days."
3. ~~HIPAA/BAA line~~ Removed per Sam.
4. **Clinic pricing.** Open. A visible TODO marker replaced "free for your clinic." The page says patients are always free. The draft plan is 3 months free, then a monthly fee. Update the page, meta and `llms.txt` once the price is set.
5. ~~Discovery calls in Charm~~ Sam is handling this. The website no longer offers them.
6. ~~/ember/ privacy line~~ Fixed. It now reads: "Your diary is stored on your phone. With Ember Plus, automatic backup encrypts your records on your phone before upload, and Ember's server never receives the key to read them."
7. **Interior utility bar.** Every page except the homepage still says "Virtual-first specialty care across Washington / In-person procedure days in Lacey, WA." Change them too if you want them to match.
8. **Remaining em-dashes in copy I didn't rewrite**: the homepage "We get it" paragraph and the Dr. Urkov quote.
9. **"Status Busters"** stays on /resources/. If you deliver it as injections, remove it along with rescue injections.
10. ~~Patient-control heading~~ Changed to "Nothing sends without the patient."
11. **Structured data.** No JSON-LD contained prices, so nothing needed updating.
12. **Before merging the landing PR**: `grep -n 'class="todo"' providers/join/index.html` must come back empty. After deploy, ping IndexNow for `/providers/join/`.

## Google Play listing

Resolves. `https://play.google.com/store/apps/details?id=com.cascadeheadache.ember` returned 200 with the listing "Ember - Migraine Tracker", developer Cascade Headache. The homepage line "Android version coming soon" was stale, so I replaced it.

## Checks run

- Chromium at 375, 768 and 1280px on home, services, resources, ember, botox, contact, drurkov and the join page: no horizontal overflow on any of them.
- Badge sizes measured as listed above.
- `grep` for discovery, rescue, sliding and the old prices across all HTML: no matches.
- No em-dashes in any added line.
- The join page form markup is byte-identical to `main`.
