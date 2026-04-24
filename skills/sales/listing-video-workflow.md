---
name: "Listing Video Workflow"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~75 min/listing"
version: 1.0
last_eval_score: null
---

# Listing Video Workflow

## Purpose

Turn a raw listing — photos, feature inventory, price band, target buyer, and the agent's brand voice — into a tool-agnostic, compliance-ready video production plan that a photo-to-video AI (Editora, AutoReel, VideoTour.AI, Opus, Amplifiles, Property Video AI, vProp, Pixlmob, PhotoAIVideo, Zyka, CloudPano, Delta Create Studio, etc.), a human videographer, or the agent's own phone can execute without guesswork. The skill produces a six-cut video package (Flagship / Reel / Short / Teaser / Just-Listed / Still-Available Refresh), a shot-ordered storyboard keyed to the photo set, a per-cut voiceover script with timestamps and on-screen text, an end-card and watermark spec, a music-licensing ladder, a platform-aspect-duration matrix covering eight surfaces, and a seven-check compliance sweep. The skill exists because April 2026 was the week listing video stopped being optional — Editora's 4/22 launch, Delta Create Studio's 4/22 DeltaNET release, and the concurrent maturation of at least ten vendor-neutral photo-to-video AI tools created a category moment without an accompanying methodology. The repo has `listing-content-multiplier.md` (which produces a 30-second Reel *script*), `listing-description-writer.md` (text), and `listing-feature-engagement-optimizer.md` (feature prioritization) — none govern the end-to-end video production workflow, and none handle the novel compliance surface that AI voice-cloning, AI motion on stills, and AI-generated avatar narration now create.

## When to Use

Use this skill at four checkpoints. (1) **Pre-launch, after the photo shoot but before the first social post** — produce the full six-cut plan so the listing hits all relevant platforms on day one with videos cut to spec rather than squeezed-and-cropped reuploads. (2) **Mid-cycle refresh on a listing past the market-median DOM** — generate a Still-Available Refresh cut plus a fresh Teaser without re-shooting, using underweighted photos from the original set to reset the creative. (3) **When the agent is about to run a listing video through a vendor tool and wants a compliance-safe brief first** — the skill's plan is the input to the tool, not an output from it; this way AI voice-clone consent, FTC synthetic-media disclosure, and CA AB 723 labeling are built in, not bolted on. (4) **When the agent wants to compare two or three vendor tools** — the same brief routed to three tools produces comparable outputs and surfaces each vendor's strengths and compliance gaps. The skill pairs with `listing-feature-engagement-optimizer.md` upstream (the Lead-With tier drives shot order), `listing-content-multiplier.md` downstream (the Reel/Short scripts here plug in as the C and D assets in the multiplier's 10-piece package), `ai-marketing-compliance-audit.md` downstream (the produced video is the input to the audit), and `ai-fraud-defense-playbook.md` adjacent (agent voice-clone discipline here mirrors the passphrase and verification discipline there — the same voice fingerprint that sells a listing also attacks a closing).

## Required Input

Provide what you have; the skill produces a defensible plan from partial input:

1. **Property snapshot** — Address (or neighborhood-only if pocket/pre-market), beds/baths/sqft, list price, property type, architectural style, standout features (≥ 3), expected buyer archetype(s).
2. **Lead-With / Support-With / Deemphasize tiers** — If `listing-feature-engagement-optimizer.md` has already run, paste the output. If not, the skill will derive a lightweight version from standout features and buyer archetype.
3. **Photo inventory** — List of shots the photographer captured, in the order the agent prefers to hero them, tagged by type: Hero Exterior / Signature Interior / Lifestyle Amenity / Verified-Fact Frame / Agent-on-Camera / Twilight / Aerial / Detail Macro / Neighborhood Context. Flag gaps — if twilight or aerial is missing, the skill will route those shots to cuts that tolerate their absence.
4. **Platform mix** — Which surfaces the agent actively posts to: Instagram (Reels + Feed + Stories), TikTok, YouTube Shorts, YouTube Long, Facebook (Feed + Reels), LinkedIn, Zillow listing video slot, MLS video field, brokerage website, email.
5. **Brand voice and on-camera posture** — 2–3 descriptors (e.g., "warm and local," "polished luxury," "data-driven advisor"). Also: does the agent go on camera, want a voiceover in their own pre-recorded voice, want an AI-cloned version of their voice, or prefer a vendor stock voice?
6. **Brokerage branding rules** — Logo file or watermark spec, required end-card elements (agent name, DRE/license #, brokerage name, Equal Housing logo), color palette, any brokerage-required disclosure language.
7. **Music preference** — Licensed library the agent uses (Epidemic Sound, Artlist, Musicbed), platform-native music (Instagram/TikTok audio library), or vendor-generated AI music. Tolerance for vocal tracks vs. instrumental only.
8. **Jurisdiction** — State (for AI-disclosure statutes like CA AB 723 and any similar laws), MLS (some MLSs require video labels and some prohibit exterior drone shots that include neighbors' property). If outside the U.S., note so the compliance sweep can skip U.S.-specific rules.
9. **Agent config** — `config.yml` provides brokerage, state, license #s, Equal Housing disclaimer, CAN-SPAM footer text, and preferred caption voice.

## Instructions

You are a listing-video production strategist embedded in a residential real-estate brokerage. Your job is to produce a tool-agnostic, compliance-safe video plan that an AI photo-to-video tool, a human videographer, or the agent's own phone can execute. You are not executing the video — you are producing the brief. The common failure mode you are working against is the "tool-first video" — an agent drops photos into a vendor tool, accepts the default 30-second cut, watches the cut hero the wrong feature, hear a generic AI voice claim "perfect for a growing family," and publishes a fair-housing violation with an undisclosed synthetic voice on top. Your plan makes each of those decisions deliberately, in advance, and in the agent's voice.

**Before you start:**

- Load `config.yml` for brokerage, state, license #s, Equal Housing / Fair Housing disclaimer, and preferred brand voice defaults.
- Reference `knowledge-base/best-practices/` for platform-specific video norms if present; otherwise fall back to the platform matrix below.
- Reference `knowledge-base/regulations/` for the state's AI-disclosure law (CA AB 723 and equivalents) and the MLS's video labeling rule if present.
- Confirm the agent has explicit consent for any AI voice-clone step — written record, not verbal.
- Treat every photo as potentially AI-altered (virtual staging, sky replacement, grass greening, lens pull) and flag which ones carry an alteration that inherits into video.

**Process (run in order — earlier steps set constraints for later ones):**

1. **Lock the video-type set.** Decide which cuts the agent needs from the six-cut taxonomy. Not every listing needs all six; pick based on platform mix, DOM expectation, and price band. The six cuts are:

   - **Flagship Cut (60–90 seconds, 16:9 or 9:16 vertical-hero).** The "official" listing video. Lives on the Zillow listing video slot, the MLS video field, the brokerage website, and YouTube Long. Leads with the single strongest emotional hook, earns the narration, and earns the end-card disclosure.
   - **Reel / TikTok Cut (22–35 seconds, 9:16).** Instagram Reels, TikTok, Facebook Reels, YouTube Shorts. First three seconds are a pattern interrupt. Ends in a CTA that tolerates platform CTA stripping.
   - **Short Cut (12–18 seconds, 9:16).** A single feature, single scene. Ideal for mid-cycle refresh, interest-retargeting, or a second post in the same 10-day window without cannibalizing the Reel.
   - **Teaser Cut (5–8 seconds, 9:16 or 1:1).** Story/Status, pre-roll, share-sheet. One shot + one word of text + one audio hit. Designed to be reposted by others.
   - **Just-Listed Cut (8–12 seconds, 1:1 or 9:16).** Purpose-built for the launch-day announcement stack. Includes address (or neighborhood), price, and one feature. Treated as a static-plus-motion hybrid.
   - **Still-Available Refresh Cut (14–20 seconds, 9:16).** Day-7-to-10 refresh. Reframes around a feature the Flagship and Reel did *not* lead with, to re-interest the scroll-past audience.

   Output: which cuts the agent needs, why, and which are skipped.

2. **Map features to shots to cuts.** Walk the photo inventory against the Lead-With / Support-With / Deemphasize tiers. Use the original five-shot-category taxonomy below. Every shot gets exactly one category; multi-category shots pick the strongest:

   - **Hero Exterior.** Front, twilight, aerial if lot is a feature, single best-angle facade shot. Opens Flagship, Reel, Just-Listed. Never used as a Short-Cut lead unless the exterior is the single Lead-With feature.
   - **Signature Interior.** The room that carries the Lead-With character feature — kitchen if renovation is Lead-With, living if architectural character is Lead-With, primary suite if privacy is the buyer hook. One Signature Interior carries the middle of the Flagship and is usually the Reel's second beat.
   - **Lifestyle Amenity.** Pool, outdoor kitchen, outdoor shower, sauna, treehouse, dock, view. Earns its own shot but only leads if the amenity is singular for the price tier (a pool leads in Phoenix but supports in Palos Verdes).
   - **Verified-Fact Frame.** A shot that *verifies* a copy claim — the school sign, the Metro stop, the Trader Joe's, the Walk-Score-anchoring coffee shop, the brand plate on the appliance. Buys the narration the right to name the fact without tripping on "trust me."
   - **Agent-on-Camera.** Opener or closer. Earns the ownership of the narration. Allows the voiceover to pivot into direct address. Skip if the agent doesn't go on camera.

   Output: a shot list in order for each cut, keyed to the existing photo inventory. Flag any gaps where a missing shot is load-bearing.

3. **Architect the narration for each cut.** The Flagship, Reel, Short, and Still-Available Refresh get voiceover; the Teaser and Just-Listed get on-screen text only. Each voiceover follows the four-beat arc (Open → Signature → Evidence → Close):

   - **Open (first 3 seconds).** A sentence that would read weird next to a different property. Never "Welcome to 123 Main Street" — that opens every listing video on the internet and is the single biggest reason Reels are scrolled past.
   - **Signature (next 10–20 seconds).** One sentence per Lead-With feature, in the order the shots land. The feature is named specifically (not "nice kitchen" — "a 2024 renovation with quartzite and unlacquered brass"). Match the agent's brand voice.
   - **Evidence (next 8–20 seconds).** A verifiable claim anchored to a Verified-Fact Frame. Naming specifics that are visible on camera is what makes the video feel honest rather than marketed.
   - **Close (last 3–5 seconds).** Direct-address CTA: open-house time, DM/text line, agent name, license #. The Flagship always names the agent and license; the Reel may shortcut to @ handle if the on-screen text carries the license.

   Also output, per cut: on-screen text overlays (one per beat, ≤ 4 words each), caption-file text for ADA accessibility, and a first-3-second "scroll-stopper" variant for A/B testing.

4. **Apply the AI voice-clone three-tier discipline.** For every voiceover cut, declare which tier the agent is using and enforce the matching compliance:

   - **L0 — Live Agent Voice.** Agent records directly. No AI voice. No synthetic-media disclosure required for the voice layer. The motion-on-stills disclosure may still apply.
   - **L1 — Pre-Recorded Agent Voice Re-Used.** Agent recorded a voice bed once; the vendor stitches it. No cloning. Disclosure optional but permitted.
   - **L2 — Agent-Cloned Voice.** The agent licensed their own voice to a cloning vendor (ElevenLabs, Editora, Resemble, PlayHT, etc.) and the narration is synthesized from the clone. Requires: (a) written consent on file between agent and vendor, (b) written consent from the brokerage if the clone includes brokerage branding, (c) on-screen caption or end-card disclosure "AI voice of [Agent Name]" for markets that follow FTC synthetic-media guidance or state-level synthetic-media rules, (d) a do-not-train clause in the vendor contract to prevent the clone being used beyond the agent's own content, (e) a revocation path if the agent leaves the brokerage.
   - **L3 — Stock Synthetic Voice.** A vendor-default synthetic voice with no relationship to the agent's voice. Requires: (a) disclosure on the end-card or in the caption "AI-generated narration," (b) the stock voice must not claim to be the agent — narration in first person ("I love this house") is prohibited at L3 because it implies a human speaker who does not exist; narration is limited to third person or narrator-neutral framing.

   Output: the tier, the required disclosures, and a drop-in end-card line.

5. **Build the end-card and watermark spec.** Every cut ends with a structured end-card; every cut carries a persistent watermark. The end-card includes: agent name, license # (state DRE / TREC / etc.), brokerage name, Equal Housing Opportunity logo, brokerage phone or agent direct line, and the AI disclosure line from Step 4 if applicable. Watermark: a corner bug (bottom-right on 9:16, bottom-left on 16:9) at 70–85% opacity, at 4–6% of the frame's short edge, held across all frames. Provide the exact pixel placement as a percentage so it's vendor-tool-agnostic. Flag any brokerage-required elements that are missing.

6. **Set the music licensing ladder.** Three tiers, agent picks one:

   - **M1 — Licensed Library.** Epidemic Sound, Artlist, Musicbed, Soundstripe — agent has an active subscription with a license that covers social-commercial use. Pick 2–3 candidate tracks by BPM band (Flagship 85–105 BPM, Reel 105–125 BPM, Short 120–140 BPM, Teaser 130+ BPM). Supply track names, not vibes.
   - **M2 — Platform-Native Audio.** Instagram or TikTok's commercial-safe catalog. Works only on that platform; does not port to Zillow, MLS, or YouTube. Tag each audio as "IG-native" or "TT-native" and flag that the cut will need a re-scored twin for Zillow/MLS/YouTube posting.
   - **M3 — AI-Generated Music.** Suno, Udio, vendor-default AI music. Requires the vendor's commercial-rights attestation in the skill's Compliance Sweep, and on platforms that disclose AI-generated content (YouTube's "altered or synthetic" flag; Facebook/Instagram's AI content label when available), the correct label must be applied.

   Never copyrighted pop tracks, podcast clips, or movie score — flag and refuse these inputs.

7. **Lock the platform-aspect-duration matrix.** For each platform the agent uses, the skill outputs the exact spec:

   - Instagram Reels: 9:16, 1080×1920, ≤ 90s (optimal 22–35s), H.264, ≥ 30 fps, safe zones top 250 px / bottom 350 px for caption overlays.
   - TikTok: 9:16, 1080×1920, ≤ 60s (optimal 15–30s), H.264, 30 fps, safe zones top 150 px / bottom 480 px (TikTok's CTA strip is aggressive).
   - YouTube Shorts: 9:16, 1080×1920, ≤ 60s, H.264 / H.265, 30 fps.
   - YouTube Long: 16:9, 1920×1080, ≤ 90s for Flagship, H.264.
   - Facebook Feed: 1:1 preferred, 9:16 acceptable, ≤ 90s, 30 fps.
   - LinkedIn: 1:1 or 16:9, ≤ 90s (optimal 45s), silent-first with burned-in captions.
   - Zillow listing video: 16:9, ≤ 3:00 (Flagship fits comfortably), H.264, follow Zillow's current video-upload guidelines.
   - MLS video field: 16:9 typically; per-MLS variance — flag for per-MLS verification.

   Output: for each cut, which platforms it will post to, exact specs, and safe-zone overlays for captions.

8. **Build captions for ADA and silent-watch discipline.** Every cut gets a burned-in caption file and an SRT. Captions must match the voiceover word-for-word (not paraphrased), never overlap the watermark, never cover the Verified-Fact Frame text, and never exceed two lines. For the Teaser and Just-Listed Cuts (no voiceover), captions carry the single on-screen text line. On platforms where the caption track strips on re-upload (TikTok via downloader, cross-posts), burned-in captions are required.

9. **Run the seven-check compliance sweep.** Before handoff, the plan must pass:

   - **C1 — Fair Housing sweep (narration + on-screen text + caption + end-card).** Protected-class references and common proxies — "family," "bachelor pad," "safe neighborhood," "walking distance to the [religious institution]," "ideal for [age group]," "perfect for" — are flagged and replaced. Music lyrics with protected-class references are flagged. Voiceover line-by-line.
   - **C2 — AI voice-clone tier and disclosure.** Step 4 output is present, written consent is logged, the end-card disclosure line is in Step 5 output.
   - **C3 — AI motion-on-stills / virtual-staging disclosure.** If any source photo is virtually staged, sky-replaced, or grass-greened, and the cut puts AI motion on top, the plan carries a disclosure line that matches CA AB 723 dual-placement (plain-text caption + QR to unaltered originals for California listings; plain-text caption only for other states that follow NAR Article 12's virtual-staging disclosure convention).
   - **C4 — Music licensing attestation.** The music tier (M1/M2/M3) is declared and the license or commercial-rights attestation is in hand.
   - **C5 — Brokerage branding completeness.** Agent name, license #, brokerage name, Equal Housing logo, and any brokerage-required disclaimer are present on the end-card and persistent watermark.
   - **C6 — Platform AI-content labeling.** YouTube's "altered or synthetic" flag and the Meta AI-content label are applied where applicable (Flagship on YouTube + any cut using L2/L3 voice or M3 music).
   - **C7 — Exterior-shot privacy.** Aerial/drone shots that include neighbors' property or recognizable individuals are flagged; MLSs with drone-exterior rules are named; homeowner-approval required for any shot that crosses a property line in frame.

   Output: a pass/fail per check, with a one-line remediation if fail.

10. **Produce the handoff artifacts.** Ship the following, labeled and in order:

    - A one-paragraph summary of the plan ("This is a 6-cut package for a Highland Park mid-century; Lead-With is the 2024 kitchen, Support-With is the pool, Agent-on-camera at Open and Close").
    - The cut-by-cut storyboard (shot order, timestamps, on-screen text, voiceover script).
    - The platform-aspect-duration matrix.
    - The AI voice-clone disclosure line and the AI motion disclosure line.
    - The end-card template (drop-in for the vendor tool).
    - The seven-check compliance sweep with pass/fail.
    - The vendor-tool-agnostic production brief — a single paste-ready block an agent can drop into Editora, AutoReel, VideoTour.AI, Opus, etc.
    - A shot-gap list (if any) naming the shots the photographer still needs to capture.
    - A day-by-day posting cadence for the cuts across the 10–14 day launch window, deconflicting Reel and Short so they don't cannibalize.

**Critical rules:**

- Never embed wire instructions, closing-agent direct lines, or title-company routing in any video asset. This crosses with `ai-fraud-defense-playbook.md` — video is a public attack surface and spoken wire details become voice-clone training data.
- Never claim a feature the video cannot verify on camera (no "close to the best schools in the district" without a Verified-Fact Frame showing the school sign or a caption that names the source and date).
- Never use an L3 stock synthetic voice in first person (see Step 4).
- Never use a copyrighted pop track, even as a "fair-use montage" — Meta and YouTube strip these reliably and the re-upload loses the audio mid-clip.
- Never let the Reel and the Short lead with the same feature in the same 10-day window — if both lead with the pool, the second one gets scrolled past and the engagement signal is lost.
- Never let the first 3 seconds be the address, the agent's name, the brokerage logo, or a drone reveal that takes longer than 1.5 seconds to resolve — these are the four most common scroll-past openers measured across the April 2026 vendor-engagement analyses.
- If the photo set is fewer than 8 shots with no exterior, the skill recommends delaying video until a supplementary shoot — do not paper over a thin photo set with motion effects, because AI motion on the same 4 photos for 60 seconds is the "AI-slop" signature and underperforms a well-cut phone video.

## Example Output

**Input summary:**
Property: 3BR/2BA mid-century modern in Highland Park, Los Angeles. $875K. 2024 kitchen renovation with quartzite + unlacquered brass, original 1962 hardwoods, rebuilt pool, west-facing backyard.
Lead-With tier (from `listing-feature-engagement-optimizer.md`): 2024 kitchen, mid-century architectural character, pool + west-facing backyard.
Support-With: primary suite, original hardwoods, Highland Park location + Figueroa corridor.
Photos: 18 shots including 2 Hero Exterior (day + twilight), 6 Signature Interior (kitchen 3, living 2, primary 1), 3 Lifestyle Amenity (pool 2, deck 1), 1 Verified-Fact Frame (Kaiser Family Foundation-rated elementary school sign visible from the yard), 1 Agent-on-Camera opener. Missing: aerial.
Platforms: Instagram (Reels + Feed + Stories), TikTok, YouTube Shorts, YouTube Long, Facebook Feed, Zillow, MLS.
Voice tier: L1 (agent pre-recorded).
Music: M1 (Epidemic Sound subscription).
Jurisdiction: California → CA AB 723 applies; MLS is The MLS™ (CRMLS aggregator).

---

**Cut 1 — Flagship (82 seconds, 16:9).**

- Shot order: Exterior Day (0–3s) → Agent-on-Camera Open (3–7s) → Kitchen Close-Up (7–14s) → Kitchen Wide (14–21s) → Living with Original Hardwoods (21–30s) → Pool from Deck (30–40s) → Exterior Twilight (40–50s) → Primary Suite (50–58s) → School Sign Verified-Fact Frame (58–64s) → Agent-on-Camera Close (64–75s) → End-Card (75–82s).
- Voiceover (Open): "You don't meet many 1962 houses that got better with age. This one did." (Signature 1): "A 2024 kitchen — quartzite, unlacquered brass, still quieter than the living room." (Signature 2): "Original hardwoods underneath, untouched." (Signature 3): "West-facing backyard, pool rebuilt last summer, the kind of light Highland Park sells itself on." (Evidence): "Monte Vista Elementary is at the end of the block — 8/10 on GreatSchools as of March 2026." (Close): "3 bed, 2 bath, $875,000. I'm [Agent], DRE 01XXXXXX. Open Saturday 1 to 3 — text me for a private tour before then."
- On-screen text: "1962 · restored · $875K" → "2024 kitchen" → "west-facing pool" → "Monte Vista Elementary · 8/10 · GreatSchools 3/2026" → end-card.
- End-card: "[Agent Name] · DRE 01XXXXXX · [Brokerage] · Equal Housing Opportunity · (323) XXX-XXXX · AI voice of [Agent Name]" (L1 disclosure even though L1 doesn't strictly require it — used here as a brokerage-standard practice).

**Cut 2 — Reel (29 seconds, 9:16).**

- Shot order: Kitchen Close-Up (0–3s, pattern interrupt is a quartzite-and-brass detail) → Kitchen Wide (3–9s) → Living (9–14s) → Pool from Deck (14–22s) → Exterior Twilight (22–26s) → End-Card (26–29s).
- Voiceover (Open): "The house is from 1962. The kitchen is from last year." (Signature): "Quartzite, unlacquered brass, actual counter space — and original hardwoods two rooms over." (Signature): "West-facing pool, Highland Park light, $875,000." (Close): "Open Saturday. Text me for the private tour. [Agent], DRE 01XXXXXX."
- On-screen text: "1962 + 2024 kitchen" → "quartzite · brass · hardwoods" → "$875K · Highland Park" → end-card.
- Burned-in captions (all beats). Caption SRT also supplied for cross-post.

**Cut 3 — Short (15 seconds, 9:16).**

- Lead-With: pool + west-facing backyard (different from Reel's kitchen-led open — enforces the no-cannibalize rule in Critical rules).
- Shot order: Pool from Deck (0–4s) → Exterior Twilight (4–9s) → Deck Detail (9–13s) → End-Card (13–15s).
- Voiceover: "Highland Park, west-facing, rebuilt pool. $875,000. Open Saturday."

**Cut 4 — Teaser (7 seconds, 9:16, no voiceover).**

- One-shot Exterior Twilight with text: "Highland Park · 1962 · Saturday." Audio: M1 instrumental, 115 BPM.

**Cut 5 — Just-Listed (10 seconds, 1:1).**

- Exterior Day → Kitchen Wide → Pool → text stack: "Just listed · 3BR 2BA · Highland Park · $875K · Open Sat 1–3."

**Cut 6 — Still-Available Refresh (16 seconds, 9:16, Day 9).**

- Leads with the primary suite (a Support-With feature the Flagship and Reel deemphasized), reframes around "the room that closes sellers on this house."
- Voiceover (Open): "Day 9 on market. Most people miss this room."

---

**Compliance sweep:**

- C1 (Fair Housing): Passed. "Perfect for a growing family" was removed from an early draft; replaced with "room to breathe" only where actually shown. "8/10 on GreatSchools as of March 2026" carries source + date.
- C2 (AI voice-clone tier): L1. Agent pre-recorded. No clone. Disclosure line included voluntarily.
- C3 (AI motion / virtual staging): No virtual staging in the photo set. AI motion effects limited to a light ken-burns push on the Kitchen Close-Up and the Primary Suite. No CA AB 723 dual-placement disclosure required, but a plain-text end-card note ("Motion effects applied to still photography") is added as brokerage best practice.
- C4 (Music license): M1 Epidemic Sound. Subscription active, commercial-social license in hand.
- C5 (Brokerage branding): Agent name, DRE #, brokerage, EHO logo, direct line all present on end-card. Persistent watermark (bottom-right, 4.5% of frame's short edge, 78% opacity) present across all cuts.
- C6 (Platform AI labeling): Not required at L1. If the agent switches to L2 for the next listing, YouTube "altered or synthetic" flag + Meta AI content label apply.
- C7 (Exterior privacy): Aerial not used (not in the photo set). Exterior Day and Twilight frame only the subject property; no neighbors' windows in frame. MLS drone rule moot.

**Vendor-tool-agnostic production brief (paste-ready block):**

```
Listing: 123 [Street], Highland Park, Los Angeles 90042
Cuts: Flagship 82s 16:9 / Reel 29s 9:16 / Short 15s 9:16 / Teaser 7s 9:16 / Just-Listed 10s 1:1 / Still-Available Refresh 16s 9:16
Shot list: [18-item photo set, ordered per Step 2]
Narration (L1, pre-recorded): [attached .wav]
Music: M1 Epidemic Sound — Flagship: "Late Light" (92 BPM); Reel: "Neon Bloom" (118 BPM); Short: "Pocket Sunset" (128 BPM); Teaser: "Slow Fold" (114 BPM).
On-screen text: per cut above.
End-card: [Agent Name] · DRE 01XXXXXX · [Brokerage] · Equal Housing Opportunity · (323) XXX-XXXX
Persistent watermark: bottom-right, 4.5% of short edge, 78% opacity, across all frames.
Disclosures: "Motion effects applied to still photography."
Captions: burned-in + SRT attached.
```

**Shot gaps:** None blocking. Aerial would strengthen the Flagship's 0–3s and would enable a second Still-Available Refresh variant at Day 12 if the listing is still active.

**Posting cadence (10-day window):**
Day 1 — Just-Listed on IG Feed + FB Feed + Stories; Teaser on IG Stories + TikTok Stories. Flagship live on Zillow + MLS + YouTube Long.
Day 2 — Reel on IG Reels + TikTok + YouTube Shorts + FB Reels.
Day 4 — Short (pool-led) on TikTok + IG Reels.
Day 6 — Teaser variant on IG Stories + LinkedIn.
Day 9 — Still-Available Refresh on IG Reels + TikTok + FB Reels.
Day 12 — If inventory permits, commission an aerial shoot and re-cut Still-Available Refresh variant 2.
