# Red-Team Report: Teacher Transition 7-Day Trial Page

**URL:** https://teachertransition.com/become-a-member-trial-1
**Domain:** page
**Brand:** Teacher Transition (`external`), detected as external, no brand profile in this workspace
**Date:** 2026-09-15
**Objective:** convert an existing free Job Board user into a card-required 7-day trial that auto-renews at $47/month
**ICP:** US K-12 classroom teachers, roughly $45K to $65K salary, already free-tier users, risk-averse about recurring charges, heavily marketed to by teacher-exit coaching operations

---

## Kill Score: 94/100

**Shipping recommendation: do-not-ship**

Ten adversaries attacked this page independently: six in-market teacher buyers carrying distinct psychological priors, three conversion-mechanics auditors, and one legal and PR risk floor. Scores ran 86, 86, 87, 88, 88, 88, 91, 92, 93, 94. The synthesizer takes the MAX, not the average, so the overall is 94.

The dominant failure is singular and structural: **this page asks for a credit card and refuses to say what it costs until the reader has scrolled 9.5 mobile screens, then makes the one price statement conditional on a coupon that does not exist anywhere on the page or in the signup modal.** Everything else compounds that. The page makes 55 promises and carries zero checkable proof for any of them: no testimonial, no customer name, no outcome number, no employer, no founder identity, no demonstration, no comparison. It then strips every reassurance it did build at the exact screen where the buyer commits, and asks for a phone number before it will show a payment option, to an audience whose live fear is being funnelled into a coaching sales call.

Nine of ten proof types are entirely absent. The tenth, the guarantee, contradicts itself inside a single card.

None of this is a polish problem. Every adversary independently reached the same place from a different direction.

---

## P0: Fix Before Ship

### P0-1: The page's core promise is conditional on a coupon that does not exist
**Flagged by:** all 10 adversaries (consensus 10)
**Location:** S5 fine print, "You'll pay $0 today when the coupon is applied."
**Why it fails:** No coupon is shown, named, auto-applied or enterable anywhere on the page, and modal step 1 has no coupon field. The literal reading is that the buyer pays $0 today only if a condition she cannot see or satisfy is met. Read that way, the default state is a $47 charge today. It is the last sentence before the final CTA and it converts the only reassuring number on the page into a new risk.
**Replacement:** Delete the conditional. If no coupon gates the trial: "You pay $0 today. There is no code to enter and nothing to apply. Your card is stored and is not charged during the 7-day trial." If a coupon genuinely gates it, show it applied in the modal: "Coupon [CODE] applied. Today's total: $0.00."
**Steelman of the opposite:** Drop the free trial entirely and sell a transparent discounted first month ($9 first month, then $47) with the price in the hero. The negative-option surface collapses, the coupon defect disappears, and a small real payment filters for intent rather than for willingness to store a card.
**Principle:** FTC Act Section 5 deception exposure on conditional price claims; risk-reversal integrity, a guarantee with an unmet condition is not a guarantee.

### P0-2: The price appears once, in grey, below the last CTA, 9.5 screens after the first ask
**Flagged by:** 10
**Location:** S5 fine print. Measured: "$47" appears exactly once on the page; mobile page height 7,704px against an 812px viewport.
**Why it fails:** A page that requires a card and withholds the number until after the ask reads as concealment, not as an offer. Any buyer converting from CTA #1 commits without ever seeing the recurring charge. On a $45K to $65K salary, $47/month is a real monthly line item and the buyer scans for a number before she reads a word.
**Replacement:** Put the full terms in body-size, body-color type directly beneath EVERY CTA: "$0 today. A card is required to start. On day 8 your card is charged $47/month unless you cancel first. Cancel in [N] clicks from your account." Add a sticky mobile bar carrying "$0 today. $47/mo from day 8."
**Steelman of the opposite:** Put the price in the H1 and lead with it: "$47 a month. Here is exactly what it buys." A product-aware free user is blocked on terms, not on desire.
**Principle:** Negative-option clear-and-conspicuous disclosure before billing information is obtained (ROSCA, FTC Act Section 5, state ARL-type statutes, applicability jurisdiction-dependent).

### P0-3: The conversion modal deletes every term the page spent 7,704px establishing
**Flagged by:** 10
**Location:** CTA modal, step 1 of 2. Verified: no price, no "$0 today", no mention of 7 days, no cancellation language, no coupon field.
**Why it fails:** Anxiety peaks where the card field is, and this is the only screen with no reassurance on it. The buyer arrives carrying the price question and the modal re-opens it instead of closing it. Every converting visitor passes through this screen.
**Replacement:** Persistent terms block at the top of both modal steps: "7-day free trial. Today: $0.00. First charge: $47.00 on [TRIAL_END_DATE]. Then $47.00 monthly until you cancel. Cancel in [N] clicks from Account, Membership, Cancel." Add an unchecked, unbundled consent checkbox gating the button: "I understand my trial converts to a paid Membership at $47/month on [DATE] and renews monthly until I cancel."
**Steelman of the opposite:** Replace the modal with a real checkout page, which has to show a price by construction and cannot become a terms-free corridor.
**Principle:** Point-of-action assurance; affirmative consent to the negative-option feature, obtained separately from other terms.

### P0-4: A phone number is required before the page will show payment options
**Flagged by:** 8
**Location:** Modal step 1, field 3, country selector plus "Phone Number...", above "Continue to Payment Options".
**Why it fails:** This ICP has been worked by teacher-exit coaching operations whose entire funnel is a booked call. A phone field on a self-serve $47 software trial, collected before a price is shown, reads as sales-call capture and confirms the grift hypothesis at the worst possible moment. It is also a TCPA exposure: a bare unlabelled field produces no consent record, and TCPA is a private-right-of-action area.
**Replacement:** Delete the field from step 1. If it is kept, label it, mark it optional, state its single purpose ("Used only to text your day-5 trial reminder. No sales calls."), and add a separate unchecked marketing-consent checkbox carrying "Consent is not a condition of starting your trial."
**Steelman of the opposite:** Pre-fill name and email for logged-in free-tier users and collect nothing at step 1 at all, since the page's own traffic assumption is that these people already have accounts.
**Principle:** Form-friction minimization; TCPA prior-express-written-consent standard for marketing calls and texts to mobile numbers.

### P0-5: The page orders you to cancel twice and never says how, and never promises to warn you
**Flagged by:** 7
**Location:** S3 card 6 ("cancel before the trial ends and pay nothing") and S5 fine print ("Unless you cancel before the end of your 7-day trial"). No cancellation mechanism appears anywhere on the page. No pre-charge reminder is promised anywhere.
**Why it fails:** For a buyer whose actual trauma is forgetting, an uninstructed cancel is a trap, not a guarantee. "Cancel before the trial ends" with no method means email support and wait, which is exactly how people get charged three months running. The deadline also has no date, no clock time and no timezone, so it cannot go in a calendar.
**Replacement:** Promote cancellation out of the feature grid into a bordered box above both CTAs: "How you cancel, in plain words. Log in. Click Billing. Click Cancel Membership. [N] clicks. No email to support, no phone call. We email you on day 5 and the cancel link is the first line. Your trial runs through [ABSOLUTE DATE] at 11:59pm [TZ]. [Add to calendar]. Cancel before then and you are charged nothing, ever."
**Steelman of the opposite:** Remove the card requirement entirely: email-only trial, ask for payment on day 7 once the product has produced something. The cancellation fear stops existing.
**Principle:** Simple-cancellation requirement under FTC negative option rulemaking and state ARL-type statutes; risk-reversal specificity.

### P0-6: Zero proof of any kind, on a page selling a career change
**Flagged by:** 10
**Location:** Whole page body, S1 through S5. Verified: zero testimonials, zero customer names, zero quotes, zero photos of real customers, zero employer names, zero outcome numbers, zero third-party validation. "Testimonials" exists only as a footer link pointing off-page.
**Why it fails:** The page makes 55 promises and substantiates none. The proof the company demonstrably owns is one click away and was left there, while the footer simultaneously boasts "thousands of teachers" and promises "inspiring success stories" the page itself does not carry. Every competing option in this buyer's tab stack, including a subreddit thread, has named humans attached.
**Replacement:** Insert a proof band between the feature grid and the final CTA: three named members, each with a photo, "[NAME], [N] years teaching [SUBJECT], [STATE]", the exact role and employer they moved into, elapsed time from joining to offer, and a verbatim quote naming which tool they used. Then one counted line with a stated denominator and response rate: "Of the [COHORT_N] members who joined between [DATES], [N] reported accepting a non-classroom role. Self-reported, [RESPONSE_PCT]% survey response. Non-responders are not counted as placements. Method: [LINK]."
**Steelman of the opposite:** Replace the whole page with one named teacher telling one story at length, resume before and after, roles applied to, the offer letter, with the CTA three times inside the story and nothing else on the page.
**Principle:** Cialdini consensus, absent entirely with the proof demonstrably existing off-page.

### P0-7: The most personal section on the page is signed by nobody
**Flagged by:** 9
**Location:** S4 H2 "What I want you to do during these 7 days", closing line "We'll help you explore the tools throughout your trial". Verified: no founder name, face, signature or bio anywhere in the page body.
**Why it fails:** A first-person request for the buyer's week and her card, from a person who will not give a name, then switching to "we" inside eight lines. In a category with a live public scam takedown, an unattributed "I" is not neutral, it is the tell. It converts the page's best-written section into evidence for the objection the page most needs to beat.
**Replacement:** Byline block at the top of S4 with a headshot: "[FOUNDER FULL NAME], [SUBJECT] teacher for [N] years in [DISTRICT, STATE], left the classroom in [YEAR], founder of Teacher Transition. [LinkedIn URL] | [direct email]". Hold first person singular through the whole section and sign it.
**Steelman of the opposite:** Rewrite S4 in plain third person as a trial plan. An unattributed personal appeal has less credibility than the same content written impersonally.
**Principle:** Cialdini authority; source attribution, an unattributed personal appeal has no authority to transfer.

### P0-8: The AI resume card carries the wrong product's copy, live
**Flagged by:** 10
**Location:** S3 feature card 3, "AI resume & cover tools". Body reads "See every curated role, not just free listings. Filter by remote, salary, experience fit, and roles that value educators." That is a verbatim duplicate of card 1's body and says nothing about resumes or cover letters.
**Why it fails:** It sits two rows under the words "Here's exactly what your free trial unlocks". The one feature that has to beat free ChatGPT describes a job-board filter instead, so the differentiator is deleted. And a visible copy-paste defect on the page that captures credit cards transfers directly onto the buyer's expectation of how a cancellation request gets handled.
**Replacement:** "Paste your teaching resume and the job posting you want. In about [T] minutes you get a rewritten resume in that posting's own language, plus a cover letter draft, editable and downloadable as .docx. Example: 'Differentiated instruction for 140 students across five reading levels' comes back as '[the actual line the tool produces]'." Add a real before and after image beneath the grid.
**Steelman of the opposite:** Cut the feature grid entirely and show the tool's actual output as the section. A demonstration of one rewritten bullet outsells six cards.
**Principle:** Hopkins specificity; credibility collapse on visible defects.

### P0-9: The page never states the one thing its audience came to find out
**Flagged by:** 7
**Location:** Whole page. No free-versus-paid comparison table, no pricing block, no counts on either side of the line. The closest attempt is S3 card 1, "See every curated role, not just free listings", which gives no number on either side.
**Why it fails:** The page's own eyebrow says the reader has already used the free Job Board. That reader has exactly one question: what does $47 buy that $0 does not. The page answers with "a taste" versus "the tools". "Curated" is used four times and is never quantified: no role count, no sourcing method, no refresh cadence, no geography, no salary band, and not one example role anywhere on the page.
**Replacement:** A two-column table in the S2 position, rows for roles visible, new roles per week, filters, fit scoring, resume rewrites, cover letter drafts, job tracker, job alerts, and price, with a real number in every paid cell pulled from the live board. Followed by three real currently-listed roles rendered at legible size with title, employer type, salary band and remote flag.
**Steelman of the opposite:** Show the inventory instead of describing it. A live scrollable feed of ten real roles with roles eleven onward blurred behind the trial gate answers the question in four seconds.
**Principle:** Schwartz awareness mismatch, the page writes Problem-Aware copy to a Product-Aware audience; upgrade-page logic, quantify the increment.

### P0-10: Two CTAs across 9.5 mobile screens, and the first one is below the fold
**Flagged by:** 8
**Location:** Whole page. Measured: 2 CTA instances, 7,704px mobile page height against an 812px viewport. At 375px the H1 alone runs about 5 lines, the hero CTA falls below the first fold, and the hero product image renders below the CTA instead of beside the copy.
**Why it fails:** One ask per 4.75 screens. Every reader convinced at the feature grid or the founder section has to scroll four more screens to act. On mobile the first screen is headline text with no button and no product, so the buyer is asked before she is shown.
**Replacement:** Shorten the H1 to two lines at 375px, reorder the mobile hero to headline, image, subhead, CTA, terms. Add a sticky bottom bar from 900px scroll depth carrying "$0 today, then $47/mo" plus the button. Add inline CTAs after the comparison table, after the feature grid and after the proof band, each with the terms line beneath it.
**Steelman of the opposite:** Kill the landing page and fire an in-product upgrade prompt on a gated action inside the free board, at the moment of blocked intent. The proof is then the user's own locked result set.
**Principle:** Conversion-path continuity, the ask must be present at every point the decision can be made.

---

## P1: High Priority

**P1-1: S2 spends the page's best slot arguing for the free product.** The section argues that generic job boards fail teachers, to an audience that already signed up for this company's teacher job board, then praises the Teacher Transition Job Board, which is the free tier. Net effect: the section argues the free tier is sufficient. Replace it with the P0-9 comparison table.

**P1-2: "Cancel anytime" contradicts its own body.** S3 card 6's title promises cancellation at any time; its body narrows it to a 7-day window with a payment consequence. Retitle to "Cancel in [N] clicks" and state the mechanism.

**P1-3: "Complete Your Enrollment" contradicts the whole offer.** The modal's second tab label is a platform default left unedited. "Enrollment" means a roster and a term to someone who has spent nineteen years in schools. Rename: "Tab 1: Your details. Tab 2: Card details ($0 charged today)."

**P1-4: The hero sells two features the page never delivers.** Floating labels "Job Alerts" and "Membership Resources / Guides and Templates" appear in the hero image and are never mentioned again, including in the section headed "exactly what your free trial unlocks". Add cards for both or strip the labels.

**P1-5: The only number on the page is unlabeled, and sits next to a zero.** The hero mockup shows "3441" with no legible label beside "Applications: 0", plus a greeting to a user named Oscar. Label the count ("3,441 curated roles live today"), populate the tracker state, and use a name matching the audience.

**P1-6: No refund text on the page.** Only a footer link and a modal link. Put the actual policy on the page in the CTA block, and commit to a post-enrolment confirmation email restating every material term.

**P1-7: Silence on data handling for a product that ingests resumes.** No statement about retention, sharing, third-party model processing, training use, or deletion, on a page whose core feature requires uploading a full employment history. A currently-employed teacher carries professional exposure risk. Add the line where the resume is ingested, and add a confidentiality statement about employer visibility.

**P1-8: The page de-scopes its own value before the buyer has bought.** S3 promises "EVERYTHING UNLOCKED FOR 7 DAYS" and S4 answers "You do not need to use every feature. You do not need to apply for 20 jobs." That is post-purchase onboarding content placed before the purchase decision, where it lowers expected value. Move it into the day-1 welcome email and put an FAQ in the slot.

**P1-9: No FAQ, so every second-order question dead-ends.** Six questions, answered on the page: when exactly am I charged, what if I forget, is my card charged today, how do I cancel, what do I keep if I cancel including my free account, who sees my information.

**P1-10: The footer hands the buyer 10 exits plus two easier free conversions.** "Free Quiz", "Our Courses", "Our Membership", "Blog", "Testimonials", plus a newsletter button placed after the final CTA. A risk-averse buyer choosing between a $47 recurring charge and a free quiz takes the quiz. Strip to Login, Privacy Policy, Refund Policy, Terms and Conditions.

**P1-11: The pay-cut fear is never addressed.** The word "salary" appears once, as a filter name. Nothing anywhere states what the destination roles pay. The household objection underneath this entire purchase is whether leaving teaching costs income, and the page talks only about money the buyer spends.

---

## P2: Polish

**P2-1: Tab title is an internal build label.** "Job Search Dashboard Signup". It is the bookmark, the background-tab label and the link preview. Rewrite: "Teacher Transition Membership: 7 days free, then $47/month".

**P2-2: Five em dashes in customer-facing copy, one of them breaking the offer.** At 375px the H1 renders as "7 days [dash]" on one line and "free." orphaned on the next. Sweep all five.

**P2-3: "Join thousands of teachers" is unquantified and promises stories the page lacks.** Either state a figure the company can produce on demand, or drop the number. Remove the "inspiring success stories" promise unless real consented testimonials ship with it.

**P2-4: Placeholder-only form fields.** Labels vanish the moment the buyer starts typing. Add visible labels above all inputs.

**P2-5: "100% Secure & Safe Payments" is asserted where no payment is collected.** It answers card-theft anxiety, which is not the fear on this page, and it names no processor. Replace with "Payments processed by [NAMED PROCESSOR]. We never see or store your card number."

**P2-6: The S3 stock photo is the category's most contaminated image.** A woman on a couch with a laptop, seen from behind, is the stock shot most attached to the coaching operations this audience has been warned about. Replace with an annotated capture of the resume rewriter mid-edit.

**P2-7: The matching feature has two different names.** "Personalized matching" in S2 and "Profile-based matching" in S3. One name everywhere, or the reader cannot count features.

---

## Complete Itemized Fix List

Every distinct fix surfaced, by location. Bracketed tokens mark a figure that must come from Teacher Transition's own data. Nothing in this list invents a number, a name or an outcome on the company's behalf.

### Hero (S1)
1. Rewrite the H1 to two lines at 375px, remove the em dash, and pull CTA #1 above the 812px fold.
2. Add the price and terms line directly beneath CTA #1, in body size and body color.
3. Label the "3441" stat tile with the metric it represents, at a size legible on a 375px viewport, or remove it.
4. Replace the "Applications: 0" empty state with a populated tracker showing real pipeline stages.
5. Change the mockup greeting name from "Oscar" to a name matching the actual audience.
6. Either deliver "Job Alerts" and "Membership Resources / Guides and Templates" in the feature grid, or remove those floating labels from the hero image.
7. Replace the "You already know" flattery opener with a countable statement of what is behind the paywall.
8. On mobile, order the hero as headline, product image, subhead, CTA, terms, so the product is seen before the ask.

### Positioning (S2)
9. Delete the "generic job boards were not built for you" argument and install the free-versus-paid comparison in that slot.
10. Replace the three text-only pills with named, countable differentiators that a free board cannot also claim.
11. Define "curated" concretely: role count, sourcing method, who screens, screening criteria, refresh cadence, geographic coverage, and the percentage of listings with a posted salary.
12. Add three to six real currently-listed roles with title, employer type, city or Remote, salary band, and one line mapping a teaching skill to the posting's requirement.
13. Add a confidentiality line: whether the buyer's search, profile and resume are visible to employers, and whether a candidate directory exists.
14. Add a salary-reality block naming what the destination roles actually pay, sourced and dated, to answer the pay-cut fear directly.

### Feature grid (S3)
15. Rewrite card 3's body to describe the resume tool's real output: what it produces, in what format, how long it takes, and whether a human reviews it.
16. Add a real before-and-after of one rewritten resume line, beneath the grid.
17. Rewrite card 2 to state what the matching is computed on and how it differs from a keyword filter.
18. Use one name for the matching feature across the entire page.
19. Quantify card 1 on both sides of the free-versus-paid line.
20. Pull cancellation out of the feature grid into a standalone bordered box above both CTAs, with the literal click path.
21. Rewrite card 5 from "onboarding tips" into an explicit pre-charge reminder commitment with a named day and a named subject line.
22. Replace the couch-and-laptop stock photo with an annotated real product capture.
23. Add the missing feature cards for job alerts and guides and templates, or remove those claims from the hero.
24. Add the free-versus-paid comparison table if fix 9 is not used.

### Founder section (S4)
25. Attribute the section to a named, photographed founder with a credential line and a signature.
26. Hold one voice throughout; remove the "I" to "we" switch.
27. Move "You do not need to use every feature" into the day-1 trial welcome email.
28. Put an FAQ answering billing mechanics into the vacated slot.

### Proof (missing section entirely)
29. Add a proof band with three named members: photo, subject and years taught, exact role and employer landed, elapsed time to offer, and a verbatim quote naming the tool used.
30. Add one counted outcome line with a stated denominator, a stated survey response rate, and an explicit statement that non-responders are not counted as placements.
31. Pull the existing off-page testimonials onto this page and stop routing proof to a footer link.

### Final CTA and fine print (S5)
32. Delete the coupon conditional and state the $0 unconditionally.
33. Restyle the fine print to body size and body color, and repeat it above both CTAs.
34. Render the charge deadline as an absolute date with clock time and timezone, plus an add-to-calendar link.
35. Put the actual refund terms on the page as readable text.
36. Commit to a post-enrolment confirmation email restating every material term, and send it.

### Conversion modal
37. Add a persistent terms block at the top of both modal steps: today $0.00, first charge amount and date, monthly renewal, cancel path.
38. Remove the phone field, or label it optional with a stated single purpose plus unbundled consent language carrying "Consent is not a condition of starting your trial."
39. Rename tab 2 from "Complete Your Enrollment" to a trial-accurate label.
40. Rename the button from "Continue to Payment Options" to carry the $0.
41. Add visible field labels above every input.
42. Add an unchecked, unbundled affirmative-consent checkbox gating the continue button.
43. Replace "100% Secure & Safe Payments" with the named payment processor.
44. Add the data-handling line at the point the resume is ingested.

### Structure and global
45. Add a sticky mobile CTA bar carrying the price, from the moment the hero scrolls out of view.
46. Add inline CTAs after the comparison table, the feature grid and the proof band, four to five total.
47. Strip the footer on this page to Login, Privacy Policy, Refund Policy, Terms and Conditions.
48. Remove the newsletter block, the Free Quiz link, and the "Our Courses" and "Our Membership" links from this page.
49. Quantify or remove "Join thousands of teachers", and remove the "inspiring success stories" promise unless stories ship with it.
50. Rewrite the browser tab title.
51. Sweep the five em dashes.
52. State plainly what the buyer keeps and loses on cancellation, including whether the free Job Board account survives.

---

## Elements That Survive

Fact framing only. These are the elements no adversary could attack.

- The S5 fine print states the renewal amount, the billing interval, the auto-continuation trigger and the payment-method requirement in a single sentence.
- The S3 card 6 body and the S5 fine print state the same renewal figure and the same cancel-before-trial-end condition, with no numeric contradiction between them.
- The trial length is stated as 7 days in the S1 H1, the S3 eyebrow, the S5 H2, both CTA button labels and the fine print, with no conflicting duration anywhere.
- Both CTA buttons carry identical label text, so the action is named the same way at both instances.
- All three content images on the page load; none are broken.
- Privacy Policy, Refund Policy and Terms and Conditions links are present in the footer, and Refund Policy and Terms are repeated inside modal step 1.
- S4 names the time-scarcity objection and answers it with four concrete alternative goals for the week. It is the only objection on the page answered head-on.
- S3 card 4 states a mechanism rather than an outcome: one place instead of scattered spreadsheets and browser tabs.
- The page body contains zero outcome claims, zero placement claims and zero earnings figures, so no endorsement or substantiation obligation attaches to the body copy as published.

---

## Adversary Breakdown

| Adversary | Kill score | One-line verdict |
|---|---|---|
| Researcher (Priya, chemistry, department data lead) | 94 | Three columns to fill, cost, what it provides, evidence it works, and after 7,704px the page filled zero of them. |
| Price-Anxious (Dana, 4th grade, $3,100/mo take-home) | 93 | The only number is a recurring charge in grey fine print 9.5 screens down, gated on a coupon that does not exist. |
| Risk-Averse (Karen, 19 years, burned by a subscription) | 92 | The screen where I hand over my card never says $47, never says 7 days, never says cancel, and calls it enrollment. |
| Spouse-Veto (Brittany, second grade, two kids) | 91 | The only sentence I can take to the kitchen table is "it's $47 a month", and that loses the argument alone. |
| Legal and PR floor (Tier C) | 88 | A card-required negative-option offer whose material terms are absent from the screen that collects the card. |
| Comparison-Shopping (Marcus, biology, seven tabs open) | 88 | Every promise here is one my other six tabs already make, and four of those tabs are free. |
| Newly-Burned-by-the-Industry (Alexis, SpEd, post-scam-thread) | 88 | First person from a person who will not give a name, asking for my phone before it will give me a price. |
| Promise-Proof Auditor | 87 | 55 promises. Zero proven. 33 asserted, 22 orphaned. Nine of ten proof types entirely absent. |
| Objection-Stack Mapper | 86 | Forty objections this buyer carries. One answered head-on, ten hand-waved, twenty-nine ignored. |
| Decision-Moment Walkthrough | 86 | It sells the free product it already gave away and hides the price it will charge. |

---

## Review Limitations

1. **External brand, no profile.** Teacher Transition is not a registered property in this workspace and has no brand profile, voice guide, VOC file or verified-claims library here. The Tier A personas were built from the page's own stated ICP and from general category knowledge, not from the company's own persona definitions. Voice critique is therefore generic direct-response principle, not brand-specific.
2. **Modal step 2 was never opened.** Filling in personal data to reach the payment screen was out of scope, so the price display, coupon handling and cancellation language at the actual card step are unverified. If step 2 restates the terms, P0-3 downgrades from critical to major. It does not rescue P0-4 or P1-3.
3. **The Tier C section is a marketer's risk review, not legal advice.** Findings are stated as exposure and remediation, never as a determination that any law has been broken. Where a state statute is named, applicability to this operator is jurisdiction-dependent and is not asserted. No citation, case, penalty figure or enforcement example was invented, and none are cited. Counsel in the operator's jurisdiction reviews before anything ships.
4. **No analytics.** This is a cold read of the live page. No traffic data, conversion rate, trial-start rate, day-8 conversion or churn figure informed any finding.
5. **No fabricated data.** Every replacement that needs a number, a name or an outcome carries a bracketed token naming the datum required. Nothing was invented on this company's behalf.

---

## Next Step

Fix P0-1 through P0-5 first: they are all billing-disclosure defects, they are cheap, and four of the five are copy changes. That alone should move the kill score materially. Then build the two missing sections, the free-versus-paid comparison and the proof band, which are the P0s that need real company data before they can be written. Re-run the red team afterwards with fresh adversaries and compare. A round that does not drop the score by at least 15 points means the fixes are not reaching the real problem, which in that case is the card-required trial structure itself.
