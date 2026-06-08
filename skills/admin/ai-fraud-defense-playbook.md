---
name: "AI Fraud Defense Playbook"
category: admin
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~30 min/incident + hours of prevented loss"
version: 2.1
last_eval_score: null
---

# AI Fraud Defense Playbook

## Purpose

Build the agent's and the brokerage's inbound-facing defense against AI-enabled fraud — voice-cloned "urgent" calls from the seller, deepfake video messages from a title officer, AI-written spoofed emails from "the lender," AI-generated identity documents on a buyer pre-qualification, AI-impersonated chat threads pretending to be an MLS admin or a cooperating agent. Produce, in one pass, a tailored defense package for a given transaction or brokerage: a transaction-level threat map, a four-tier verification ladder, a set of original live-challenge prompts a deepfake is unlikely to pass, a passphrase protocol, a wire-instruction-change standard operating procedure, a client-facing one-pager, a brokerage training cadence, and — if a suspected-fraud incident has already started — a time-boxed incident response checklist. The skill exists because the compliance stack (`ai-marketing-compliance-audit.md`) governs *outbound* AI content; nothing in the repo covers *inbound* AI impersonation. April 2026 industry coverage crystallized the gap: FBI reported $275M in real-estate-related cybercrime losses in 2025, Business Email Compromise ranked #2 at $3.04B, voice-clone and deepfake-video scams are now routinely reported against closings, and 60%+ of deepfake attempts cluster in the 72 hours before wire instructions are sent. The playbook treats inbound fraud as a predictable operational risk with predictable choke points, not an exotic event.

**v2.1 expansion (June 2026).** Two same-week industry sources widened the inbound attack surface this playbook must cover. (1) Fidelity National Financial's chief innovation officer documented how organized rings now combine fabricated identity documents that pass automated credential checks with a deepfake video overlay on the **remote online notarization (RON)** call — a vector that defeats the standard digital-verification stack and is caught primarily by trained human judgment, not software. (2) HomeLight's Q2 2026 Top Agent Insights report (950 agents surveyed) surfaced the **agent as a direct target**: malicious "buyer Zoom links" that install malware and steal credentials, after which the agent's own compromised account is used to attack their clients. The FBI's 2025 IC3 report refreshed the loss anchors — 1,008,597 cyber-crime complaints / **$20.8B total losses (+26% YoY)**; real-estate fraud **12,368 complaints / $275.1M** (up from 9,359 / $173.6M the prior year); **22,000+ AI-referenced complaints / $893M** adjusted losses; victims **60 and older lost $7.7B (~60% YoY jump)**, making long-tenured and absentee owners the highest-value seller-impersonation target pool. v2.1 adds a LISTING-INTAKE checkpoint, a RON physical-liveness challenge protocol, a meeting-link malware rule, and a county-recorder fraud-alert preventive step. The deeper structural v2 rewrite (three fraud-vector classes — traditional-wire / email-document / crypto-rail — plus the Cotality client-one-pager framing) remains queued.

## When to Use

Use this skill at six checkpoints: (0) **Listing intake** — *before* representation is signed, when an inbound "seller" solicits a listing on **vacant land, an absentee-owner property, or a long-tenured / elderly owner's home** (the three highest-fraud-rate categories per the NAR 2025 Deed & Title Fraud Survey: vacant land 62% of reported title-fraud cases, owner-occupied homes 12%, detached single-family 16%). The seller-impersonation fraudster's entry point is the listing solicitation itself; the defenses here are independent-public-data identity cross-checks and a title-partner pre-screen, run before the agent invests in the listing. (1) **Transaction kickoff** — generate the per-deal defense package the moment a buyer or seller signs representation, when the passphrase is cheapest to establish and the client is most receptive to a 2-minute safety briefing. (2) **The 72-hour window before funds move** — the highest-risk interval; run a targeted refresh of the verification ladder for this deal and confirm the wire-instructions SOP is primed. (3) **Any inbound message that changes money, routing, or a named counterparty** — new wire instructions, a new closing agent, a new title company, a new lender contact, a substitute notary, a change in POA, a "different account" ACH update. (4) **Quarterly brokerage training** — produce the drill script, the red-team simulated-call plan, and the post-drill scorecard. (5) **Active incident** — a suspicious call, email, or deepfake is already in play; produce the immediate-action checklist with the clock running. The skill is complementary to `ai-marketing-compliance-audit.md` (outbound content governance) and `transaction-coordinator-brief.md` (happy-path TC workflow), and hands off cleanly to both — when a finding materially changes a transaction, it updates the TC brief; when it touches brokerage policy, it loops the compliance audit cycle.

## Required Input

Provide what you have; the skill produces a defensible defense package from partial input:

1. **Mode** — `LISTING-INTAKE` (inbound listing solicitation on vacant-land / absentee-owner / long-tenured-owner property, pre-representation) / `KICKOFF` (new transaction) / `PRE-WIRE` (72-hour window) / `CHANGE-EVENT` (inbound request changes money or routing) / `TRAINING` (brokerage drill) / `INCIDENT` (suspected active fraud). Mode controls which output sections the skill emphasizes.
2. **Transaction snapshot (for KICKOFF / PRE-WIRE / CHANGE-EVENT / INCIDENT)** — Address, list/purchase price, buyer and seller names, listing agent, buyer's agent, brokerage(s), title/escrow company, lender, closing date, funds-transfer date, current status (listed / under contract / cleared to close / funding / post-close).
3. **The inbound event (for CHANGE-EVENT / INCIDENT)** — The message itself (voicemail transcript, email, text, chat, video link), the channel it arrived on, the sender's stated identity, the specific action requested, the urgency framing, any attachments, any prior legitimate communication this could be spoofing.
4. **Relationship context** — How the client prefers to be contacted, their typical reply latency, any known vulnerabilities (first-time buyer, senior client, client out-of-country during closing, client who previously fell for a phishing email).
5. **Counterparty verification anchors** — Known-good phone numbers (not pulled from emails), direct-line numbers for title officer / escrow officer / lender rep / listing agent / buyer's agent, brokerage's fraud-ops mailbox, broker-of-record direct line, state RE commission fraud-reporting contact. If `config.yml` has a `known_good_lines` section, the playbook auto-loads the brokerage's standard direct lines (title / escrow / lender / co-op agent / broker-of-record / brokerage IT / state RE commission fraud line) and only re-prompts the agent for transaction-specific lines (the actual title officer assigned to this deal, the lender rep for this loan). Reduces a per-run friction point that previously required the agent to type the same six numbers on every kickoff.
6. **Jurisdiction** — State (two-party-consent rules, state RE commission reporting thresholds, state-level AI-impersonation statutes if applicable), MLS (some MLSs now require deepfake-incident reporting), county recorder (for quitclaim / title-theft angle).
7. **Brokerage AI Use + Fraud Policy (optional)** — If the brokerage has a written wire-fraud or AI-impersonation SOP, paste it. The playbook will cross-check and, where brokerage policy is stricter, follow brokerage.
8. **Agent config** — `config.yml` provides brokerage, state, license numbers, preferred client-facing language, and the escalation chain.

## Instructions

You are a senior fraud-operations specialist working inside a real-estate brokerage. Your job is not to perform law enforcement or provide legal advice. Your job is to reduce the probability that a fraudulent inbound message converts into a loss by (a) making the expected defenses explicit before anyone is under pressure, (b) removing the ambiguity that attackers exploit ("did she say change the account, or keep the account?"), and (c) forcing a small number of hard stops at the moments where money and trust actually move. Where the input is ambiguous or the jurisdiction is unclear, say so plainly and route to broker-of-record.

**Before you start:**

- Load `config.yml` for brokerage, state, license numbers, known-good phone numbers, and escalation chain.
- Reference `knowledge-base/compliance/` and `knowledge-base/best-practices/` for brokerage-specific rules if present.
- Identify the transaction's risk profile: price band, closing-date proximity, out-of-state or out-of-country counterparty, prior change-events on this deal, and whether the clients have been trained on the passphrase.
- Treat urgency framing ("must happen today," "don't mention this to anyone") as a hostile signal, not a legitimate constraint.

**Process (run in this order — order matters because earlier findings set the verification tier for later steps):**

1. **Select the mode and scope.** Lock in which of the five modes applies (KICKOFF / PRE-WIRE / CHANGE-EVENT / TRAINING / INCIDENT) and what output sections are relevant. Modes are not additive by default — a KICKOFF run does not produce the INCIDENT checklist unless the caller explicitly requests both.

2. **Build the transaction-level threat map.** For this specific deal, enumerate the "trust triggers" — moments where a single message can move money, change a named party, or reroute documents. Typical triggers (tailor to the deal):
   - Wire-instruction delivery from title / escrow
   - Wire-instruction *change* after the original delivery
   - Substitute closing agent, notary, or signing location
   - New lender rep or loan-officer handoff
   - Buyer POA or seller POA activation
   - Seller proceeds re-routing ("send my half to this account instead")
   - Earnest money deposit updates
   - Inspection or appraisal routing changes
   - Post-close rent-back rent payment routing
   - Commission re-assignment ("pay the referral to this new account")
   - **Listing solicitation from a "seller" on vacant land / absentee-owner / long-tenured-owner property** (LISTING-INTAKE) — the seller-impersonation entry point; the "owner" who can't easily be reached at the property, whose contact details match the public listing record but whose identity has not been independently confirmed
   - **Remote online notarization (RON) signing call** — a video-notarization session where a deepfake overlay + AI-fabricated government IDs are used to impersonate the seller/grantor at the moment of signing
   - **Inbound video-meeting link from a "buyer" or counterparty** — a Zoom/Teams/Meet link that, when clicked, installs malware or harvests credentials rather than opening a meeting; the agent (not the client) is the direct target
   For each trigger, tag it with likely attack vectors: voice clone, deepfake video (including RON-call overlay), AI-written spoofed email, AI-generated doc (fake ID, fake wire confirmation, fake lender statement, forged deed/notary seal), chat/SMS impersonation, social-engineered helpdesk reset, malicious meeting-link credential-harvest.

   **Threat-Map Dollar-Weight column.** Tag each trigger with the loss-anchor benchmark for its attack vector class, so the threat map prioritizes by *expected loss* rather than equal weighting. Use the FBI IC3 2025 + Entrust Identity Fraud Report 2025 anchors below; replace with brokerage-specific actuals if available:

   | Attack vector class | Loss anchor | Source |
   |---|---|---|
   | Business Email Compromise (wire-fraud, real-estate sector) | **$275M annual sector loss** (FBI IC3 2025); BEC overall **$3.04B annual** (#2 cybercrime category); per-incident median **$50K–$200K** for residential closings, escalating into mid-six-figures for commercial | FBI IC3 Internet Crime Report 2025 |
   | Voice-clone (live-call impersonation) | Per-incident median **$43K**; cluster of incidents in the **72 hours before wire**; first-named live-call-detection vendor category emergent May 2026 (Diopter AI) | FBI IC3 2025 + Entrust Identity Fraud Report 2025 |
   | Deepfake video (synthetic-presenter "title officer," fake closing agent on Zoom) | Sub-$1M total recorded sector loss in 2025 (small N), but **per-incident loss high** when it lands; trajectory steeply upward in Entrust 2025 longitudinal series | Entrust Identity Fraud Report 2025 |
   | AI-generated identity document (buyer pre-qual, POA spoofing) | Embedded inside BEC + sector reporting; flagged as **fastest-growing AI fraud vector** in Entrust 2025 (>3,000% YoY in covered domains) | Entrust Identity Fraud Report 2025 |
   | Helpdesk / SMS impersonation (substitute notary, MLS admin spoof) | Embedded inside the FBI BEC total; methodology-relevant because it bypasses the email channel entirely and lands on whichever channel the agent treats as trusted | FBI IC3 2025 |
   | Deed / seller-impersonation fraud (listing-intake + RON-call) | Concentrated in **vacant land (62% of cases)**, owner-occupied (12%), detached SF (16%) per NAR 2025 survey; **elderly 60+ lost $7.7B (~60% YoY jump)** and are the prime impersonation target pool; per-incident loss = full sale proceeds when it lands | NAR 2025 Deed & Title Fraud Survey + FBI IC3 2025 |
   | Malicious meeting-link credential-harvest (agent as direct target) | Embedded inside the broader BEC/cyber total ($20.8B, +26% YoY); methodology-relevant because the loss is *second-order* — the compromised agent account is then used to run BEC against that agent's whole client book | FBI IC3 2025 + HomeLight Q2 2026 Top Agent Insights |

   **Triage rule:** if two triggers compete for verification capacity inside the 72-hour pre-wire window, the one with the higher loss anchor escalates first. A wire-instruction-change trigger (BEC, $50K–$200K typical) outranks a routing change on inspection or appraisal (low expected loss). The dollar-weight column is the source of truth for that decision.

3. **Assign each trigger a verification tier on a four-tier ladder.** The ladder exists because verification cost is not free; apply it where it pays off. Use:
   - **L0 — Pass-through.** Communication is routine, no money or routing changes, counterparty is previously verified, channel is the previously verified channel. Proceed normally; log only.
   - **L1 — Out-of-band callback on a known-good number.** Any inbound email, SMS, or voicemail that requests a change to money, routing, or a named party. Callback uses a number pulled from the original engagement packet or the counterparty's public license record — never from the inbound message. Document the callback time, the number dialed, and who answered.
   - **L2 — Live challenge + secondary channel confirmation.** Anything that (a) touches wire instructions, (b) introduces a new counterparty, (c) is accompanied by urgency framing, or (d) the L1 callback was inconclusive. Requires a live challenge (below) on the call, plus confirmation via a second independent channel — e.g., DocuSign link, in-person drop-by, or verified brokerage portal.
   - **L3 — Hard stop, freeze, escalate.** Suspected active fraud, any mismatch on L2, any attempt by the counterparty to discourage callback, any attempt to substitute the brokerage-side contact, any pressure to bypass the SOP. No funds move. Pull the broker-of-record, escalate to counsel, and preserve the inbound artifact (recording, full email headers, link, screenshots).

4. **Generate the live-challenge prompt set.** Produce 6–10 original, deal-specific questions that require knowledge only a legitimate counterparty would have from prior transaction correspondence. Draw on: an irrelevant conversational detail from the last legitimate call (weather, a joke, the color of the front door), a specific number that did *not* appear in any public document (the exact earnest money cents, the notary's middle initial, the number of pages in the inspection report), a logistical detail that is trivially verifiable but not guessable (where the next meeting was last scheduled). Avoid questions whose answer is on the public MLS record, Zillow, or the brokerage website. Rotate the questions across calls so prior calls cannot be used to train a clone. Never write the challenge questions into the inbound email or text; deliver them verbally only.

   **Physical-liveness challenge (for any live video call — RON signing, "title officer on Zoom," "buyer/seller verification call").** Knowledge questions test what the persona *knows*; the liveness challenge tests whether the *image itself* is real-time and unmodified. A deepfake video overlay degrades under motion and occlusion that the model was not trained to render. On any video call where identity matters, ask the person to perform a short, unscripted sequence of physical movements and watch the image for distortion, smearing, edge artifacts, or lag:
   - Slowly pass a hand fully in front of the face and away again (occlusion breaks most overlays at the hand/face boundary).
   - Remove and replace glasses; turn the head to full profile, left then right.
   - Stand up and step back from the camera, then return.
   - Hold a government ID up next to the face and rotate it (tests both the ID and the face-to-document match in the same frame).
   Vary the requests so the sequence cannot be pre-rendered. **Treat any image disruption — even momentary — as an L3 hard stop**, not a connection glitch to wave through. This is the technique FNF's processors used to catch an AI-generated overlay on a notarization call that had already passed automated credential checks: the IDs and the backstory were perfect; the image broke when the "seller" was asked to move. Human judgment caught what the automated stack could not. Where a vendor live-call/liveness-detection tool is in use, its verdict is an L2 augmentation signal only (see Critical Rules) — it never replaces the human watching the image during the movement sequence.

5. **Establish or refresh the passphrase protocol.** Produce:
   - A client-facing passphrase setup script for KICKOFF (2 minutes at signing).
   - A rule that the passphrase is shared in person or on the first verified phone call — never in email, SMS, or video recording.
   - A rule that any request to "change" or "update" the passphrase is treated as an L3 hard stop until confirmed in person.
   - A rule that the passphrase is requested on every inbound call that touches money or routing, not only on suspicious calls — so its absence on a suspicious call is a signal rather than a tip-off.
   - A rotation policy: passphrase resets at each transaction stage (representation signed → contract signed → cleared to close → post-close) to limit exposure if a prior stage's communications are compromised.

6. **Draft the wire-instructions SOP.** Produce a single-page procedure the agent and client follow at the funds-transfer moment:
   - Title / escrow delivers wire instructions via the brokerage's verified portal, not by email attachment or embedded link.
   - Client receives instructions directly from title, not forwarded by the agent.
   - Any change to those instructions — any change, including a digit of the account number, a new routing number, a new receiving bank, a new memo line — triggers L2 minimum.
   - Callback is made to a phone number on the title company's state-licensing record or on the engagement letter, never to a number in any email signature.
   - A 24-hour waiting period applies to any late-cycle change-request inside the 72-hour pre-wire window unless broker-of-record explicitly overrides in writing.
   - Wire-confirmation message from the bank is verified by the agent and the client before closing is called "funded."

7. **Draft the client one-pager.** Produce a plain-language one-pager (≤ 300 words) the agent sends the client at KICKOFF. Cover: the three scams they will most likely face (voice clone, wire-instruction change, fake lender email), the passphrase, the two "never-do" rules (never wire without a verified callback, never act on urgency without confirming in person or on a known-good number), and the brokerage's direct line for suspicious messages. Written at ~8th-grade reading level; no jargon; one-sided so it can be printed and handed out.

8. **Draft the brokerage training artifacts (TRAINING mode).** Produce:
   - A quarterly drill script: a realistic voice-clone scenario the broker-of-record runs on one agent per cycle.
   - A red-team simulated-call plan: three scripted calls (wire change, substitute closing agent, urgent seller callback) for a compliance proctor.
   - A post-drill scorecard with six dimensions (verification, callback discipline, passphrase discipline, escalation, documentation, client handling).
   - A hotwash template (what caught it, what almost didn't, what changes).

9. **Run the incident-response checklist (INCIDENT mode).** If the caller is mid-event, produce a time-boxed response with clearly labeled phases and owners:
   - **T+0:00 — Stop.** No funds move. No replies to the suspect channel. No clicks on any link. Do not confront the suspected actor.
   - **T+0:05 — Preserve.** Screenshot every frame; save the full email with headers (File → Save As EML, not a forwarded copy); save any attachment to a non-executing file viewer; capture voicemail as an audio file, not a voicemail transcription.
   - **T+0:15 — Notify the actual counterparty.** Call the title officer / lender / cooperating agent on a known-good number to confirm whether the suspect message is legitimate. If not, they will also want to be in the loop because the attacker may be mid-attempt against another of their clients.
   - **T+0:30 — Broker-of-record + brokerage IT.** Escalate in writing; broker decides whether counsel is looped.
   - **T+1:00 — Client.** If the client received the same message, call them on the known-good number with the passphrase to verify they are not mid-action.
   - **T+4:00 — Report.** FBI IC3 (ic3.gov), state RE commission (if the message impersonated a licensee), state AG consumer-fraud line, bank (if any funds already moved). If funds moved, time is the governing variable — banks can sometimes claw back within ~72 hours.
   - **T+24:00 — Post-incident review.** Run the hotwash; update the brokerage SOP; notify adjacent transactions where the same attacker may be active.

10. **Map compliance and data-handling overlay.** Every output checks against: NAR Code of Ethics Article 1 (duty to protect/promote client interest), state RE advertising/representation rules, Gramm-Leach-Bliley Act data-handling for any financial information collected in the course of verification, FTC Safeguards Rule (brokerage-as-covered-entity), state two-party-consent recording rules where the callback is recorded (currently: CA, FL, IL, MD, MA, MT, NV, NH, PA, WA, plus others with recording restrictions). Where the recording is made, get consent on the line before substantive questions. Where jurisdictional ambiguity exists, say so and route to broker-of-record.

   **State-Specific Recording-Consent Scripts (ready-to-paste).** For an L1 callback in a two-party-consent state, open with the state-appropriate disclosure line below — recorded before substantive questions, on the line, so the recording itself captures the consent. Statute cites are for the SOP file; the script is what the agent says:

   | State | Opening line | Statute |
   |---|---|---|
   | **CA** | "Before we begin, I'm recording this call for fraud-verification purposes. Is that okay with you?" | Cal. Penal Code § 632 |
   | **FL** | "I'd like to let you know I'm recording this call for fraud-verification purposes — please confirm you're okay with that before we continue." | Fla. Stat. § 934.03 |
   | **IL** | "I'm going to record this conversation for fraud-verification purposes. Do I have your consent to record?" | 720 ILCS 5/14 (Eavesdropping Act) |
   | **MD** | "This call is being recorded for fraud-verification purposes. May I have your consent to continue the recording?" | Md. Code Cts. & Jud. Proc. § 10-402 |
   | **MA** | "I'm letting you know this call is being recorded for fraud-verification purposes — is that okay with you?" | Mass. Gen. Laws ch. 272 § 99 |
   | **MT** | "I'm recording this call for fraud-verification purposes. Do you consent to the recording?" | Mont. Code Ann. § 45-8-213 |
   | **NV** | "This call is being recorded for fraud-verification purposes. Please confirm you consent to recording." | Nev. Rev. Stat. § 200.620 |
   | **NH** | "I'm recording this conversation for fraud-verification purposes. Do you consent?" | N.H. Rev. Stat. § 570-A:2 |
   | **PA** | "I'm recording this call for fraud-verification purposes. Do I have your consent to record?" | 18 Pa. C.S. § 5704 (Wiretap Act) |
   | **WA** | "This call is being recorded for fraud-verification purposes. Do you consent to being recorded?" | Wash. Rev. Code § 9.73.030 |

   **One-party-consent states (all others):** disclosure is courteous-but-not-required if the agent is a party to the call; the SOP recommendation is still to open with a brief recording-purpose statement so the recording is admissible across forums and so the counterparty understands the verification posture is procedural, not adversarial.

   **If consent is refused:** the call continues *without* recording, but the L1 callback now also triggers an L2 escalation note — a counterparty who refuses recording on a verification call is, by policy, treated at L2 verification minimum until the L2 challenge passes. Document the refusal and the L2 escalation in the verification log.

**Critical rules:**

- This skill does not replace the brokerage's E&O policy, cyber-insurance, or legal counsel. It produces procedural defense, not legal advice.
- Urgency is always a signal, never a constraint. Any "must happen today" request is treated at L2 minimum.
- Never write challenge questions or the passphrase into any asset that leaves the agent's direct control (no email, no CRM memo the client can see, no shared doc).
- Callback numbers come from the engagement letter or the public licensing record. Numbers in email signatures, email bodies, voicemail callbacks, or text messages are not "known-good."
- A counterparty who resists callback verification is, by policy, not a legitimate counterparty until proven otherwise.
- Document every verification decision. A clean L0 is still logged. "I felt it was fine" is not a record.
- Do not tip off the suspected actor during a live incident. The goal is to preserve evidence and protect the client, not to confront.
- Fraud defense language to clients never blames the client. The one-pager and scripts assume a sophisticated attacker, not a careless client.
- For incidents involving suspected deepfake audio or video, preserve the original file and its metadata; AI-forensic review depends on metadata that is destroyed by re-encoding.
- Live-call deepfake-detection tooling is a newly named vendor category as of May 2026 (Diopter AI is the first named entrant targeting the closing-table verification call surface, scoring authority / urgency / isolation / escalation / ask signal-arcs across a live call rather than analyzing isolated frames). Treat such tooling as an **L2 augmentation signal** — useful as one of multiple inputs into the verification tier decision — and explicitly **not** an L1 substitute. A clean detection score never replaces the out-of-band callback on a known-good number; a flagged score upgrades the trigger to L3 (hard stop, freeze, escalate). Where the brokerage has procured a live-call detection tool, document its score and verdict alongside the callback record in the verification log; where it has not, the absence is itself a documentation note ("no live-call detection tooling in use; verification rests on callback + live-challenge + secondary-channel confirmation"). The category is methodology-relevant whether or not the brokerage subscribes — the existence of vendor-grade detection raises the bar on what counts as "reasonable defense" in any post-incident review.
- **Never click a meeting link the counterparty supplies.** The agent originates and sends every video-call link; an inbound "here's my Zoom link" from a buyer, seller, or new counterparty is treated at L2 minimum and is sandboxed/scanned by brokerage IT before opening if it must be opened at all. The agent — not the client — is the high-value target for credential theft, because a compromised agent account becomes the launchpad for BEC against the agent's entire client book.
- **Listing-intake identity cross-check (vacant land / absentee / long-tenured owner).** Before investing in a listing solicited by an inbound "owner," verify identity against *independent* public-record sources — addresses, phone numbers, and emails that did **not** originate with the person soliciting the listing — rather than confirming the seller's details against the very contact information they supplied (which a fraudster controls). Loop the title partner for a pre-listing identity pre-screen; a multi-state title underwriter sees impersonation patterns a local-only operation never will. Recommend the true owner register the property with the **county recorder's free fraud-alert / property-watch notification** where offered (especially for vacant or unmonitored parcels). When the property record shows a deed recorded with no sale behind it, or a notary seal the brokerage can verify by calling the notary directly, treat the chain-of-title anomaly as an L3 escalation to the title partner before proceeding.
- **Image disruption on any verification video call is an L3 hard stop**, never a "bad connection" to push past. The liveness challenge exists precisely because the automated credential stack can be defeated; the human watching the image during the movement sequence is the control.
- Training drills are announced as drills to the client if a client is involved; simulated calls to clients are not acceptable without written consent and broker-of-record sign-off.

**Output structure (sections included depend on mode):**

1. **Mode + Scope** — one line stating which mode is running and which sections follow.
2. **Transaction Threat Map** (LISTING-INTAKE / KICKOFF / PRE-WIRE / CHANGE-EVENT / INCIDENT) — enumerated trust triggers and assigned attack vectors. In LISTING-INTAKE mode, the map centers on the seller-impersonation entry point and the independent-public-data identity cross-check rather than the wire-transfer choke points.
3. **Verification Ladder Assignment** — per trigger, the tier (L0/L1/L2/L3) with the rule that puts it there.
4. **Live-Challenge Prompt Set** — 6–10 deal-specific questions, rotated per call.
5. **Passphrase Protocol** — setup script, rotation schedule, usage rule.
6. **Wire-Instructions SOP** — one-page procedure.
7. **Client One-Pager** (KICKOFF) — ≤ 300 words, plain language.
8. **Brokerage Training Artifacts** (TRAINING) — drill script, red-team plan, scorecard, hotwash template.
9. **Incident Response Checklist** (INCIDENT) — time-boxed T+0:00 → T+24:00 actions with owners.
10. **Compliance + Data-Handling Overlay** — jurisdictional flags, recording-consent reminders, broker-of-record triggers.
11. **Known Gaps + Human-Review Items** — things the skill could not verify and routes them to broker-of-record or counsel.

## Example Output

**Mode + Scope:** `CHANGE-EVENT` — inbound email dated 2026-04-23 08:47 local, purporting to be from escrow officer Priya Rao at Western Title, requesting buyer to re-wire earnest money to a "corrected" account ahead of 10:00 am cutoff.

**Transaction Threat Map (4821 Laurel Canyon Blvd, Studio City, CA — $1.485M, closing 2026-04-30):**

| # | Trust Trigger | Deal Status | Attack Vector Likely |
|---|---|---|---|
| 1 | Earnest money re-wire | Under contract, funds already delivered to original account | AI-written spoofed email with "corrected" account |
| 2 | Final closing wire (buyer funds) | T-7 days | Voice-clone call in 72-hour window |
| 3 | Seller proceeds routing | T-7 days | AI-written spoofed email from "seller" to escrow |
| 4 | Substitute notary / signing location | Scheduled | Deepfake video from "title" re-routing |
| 5 | Commission re-assignment | Post-close | AI email to brokerage accounting |

**Verification Ladder Assignment (for the 2026-04-23 inbound event):**

| # | Action Requested | Tier | Rule |
|---|---|---|---|
| 1 | Re-wire earnest money to new account | **L3 — Hard stop** | Late-cycle change-request + urgency framing + account substitution inside the 72-hour window. Freeze. |
| 2 | Subsequent L2 verification (once frozen) | L2 | Callback to Priya Rao at Western Title on the number from the engagement packet (not in the email). Live challenge. DocuSign portal confirmation. |

**Live-Challenge Prompt Set (rotated; choose 3 for this call):**

1. "What was the exact earnest-money figure down to the cents?" (Answer on file: $29,700.00 — the .00 is the tell; an AI persona will often guess $29,700 even.)
2. "In our last call on 4/18, what did you mention about your drive home?" (Live detail from the prior verified call.)
3. "Who is copied on the closing disclosure besides me, [buyer], and [seller]?" (Answer on file: the lender's funding specialist — not a name on the public record.)
4. "What's the code on the lockbox we used at the inspection?" (Answer the cooperating agent would know; changes per inspection.)
5. "What font does your escrow-instruction PDF use in the header?" (Legitimate vendor answers without hesitation; cloned persona typically can't.)
6. "Read me the last four of the wire-reference number on the first delivery — the original, not the one you just sent."

**Passphrase Protocol:** Passphrase on file (set at KICKOFF 2026-03-14): **[REDACTED — known only to agent + buyer; not written in this report]**. Rotation scheduled for "cleared to close" stage. Any request from "client" or "counterparty" to set, reset, or share the passphrase over email is L3.

**Wire-Instructions SOP (excerpt):**

- Original instructions delivered via Western Title's verified portal on 2026-03-21. Portal URL on file.
- Any change must come through the same portal AND be callback-verified.
- 24-hour waiting period applies to the requested change-event above. The 10:00 am cutoff claimed by the suspect email is not a legitimate constraint and is, in fact, evidence of attacker pressure.

**Client One-Pager:** [Generated separately; not relevant for CHANGE-EVENT mode.]

**Incident Response Checklist (in effect — current T+0:12):**

| Time | Action | Owner | Status |
|---|---|---|---|
| T+0:00 | Freeze funds — no replies, no clicks | Agent | Done 08:49 |
| T+0:05 | Preserve: save EML with full headers, screenshot, capture any linked PDF without opening | Agent | Done 08:53 |
| T+0:15 | Call Priya Rao on engagement-packet number (310-555-0188), not email-signature number | Agent | In progress |
| T+0:30 | Notify broker-of-record + brokerage IT; preserve original EML to compliance mailbox | Agent → BoR | Pending |
| T+1:00 | Call buyer on passphrase-verified known-good number; do not send the suspect email to buyer; warn them of any similar inbound | Agent | Pending |
| T+4:00 | Report: IC3.gov; CA DRE if the message impersonated a licensed escrow officer; buyer's bank if any funds moved (none yet) | BoR / Agent | Pending |
| T+24:00 | Hotwash; SOP update; check whether any other deal in the brokerage has been hit in the past 72 hours | BoR | Pending |

**Compliance + Data-Handling Overlay:**

- California is a two-party-consent state. The callback to Priya will be recorded; consent will be obtained on the line before substantive questions ("I'm recording this call for fraud-review purposes — is that okay with you?").
- Preserve original email EML; a forwarded copy loses header metadata that IC3 and the brokerage IT team will need.
- Broker-of-record notification is non-optional at L3. Document the decision chain.
- FBI IC3 report is recommended regardless of whether funds moved; industry pattern data depends on reporting volume.
- NAR Code of Ethics Article 1 (duty to protect/promote client interest) is active; failing to escalate is a duty-of-care exposure, not only a best-practice miss.

**Known Gaps + Human-Review Items:**

- The suspect email's headers show a display-name match but I have not independently verified the full `Received:` chain or DKIM/DMARC status. Route to brokerage IT for header analysis.
- I cannot confirm from the inputs whether the earnest money is still fully at the original account or has been partially moved. Agent to confirm balance with original account-of-record before the callback concludes.
- California AB 2930 / proposed state-level AI-impersonation statute language is still being refined at publication date; if this incident results in litigation or an insurance claim, verify current statute with counsel.
- If Priya Rao on callback confirms the email is not from her, she is also a victim and should be encouraged to loop her own firm's incident-response team. The attacker is likely mid-campaign.
