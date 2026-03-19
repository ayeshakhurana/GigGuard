# 🛡️ GigGuard — Parametric Income Insurance for India's Gig Delivery Workers

> **DEVTrails 2026 · Phase 1 Submission**
> Instant, condition-triggered income protection for food delivery partners — built to pay the honest and catch the fraudulent.

---

## Table of Contents

- [Problem Statement](#problem-statement)
- [Our Chosen Persona](#our-chosen-persona)
- [Persona-Based Scenarios & Application Workflow](#persona-based-scenarios--application-workflow)
- [Weekly Premium Model, Parametric Triggers & Platform Choice](#weekly-premium-model-parametric-triggers--platform-choice)
- [AI/ML Integration Plan](#aiml-integration-plan)
- [Tech Stack & Development Plan](#tech-stack--development-plan)
- [Adversarial Defense & Anti-Spoofing Strategy](#adversarial-defense--anti-spoofing-strategy)
- [Phase 1 Prototype Scope](#phase-1-prototype-scope)
- [Repository & Demo](#repository--demo)

---

## Problem Statement

India's 12 million+ gig delivery workers are the backbone of our digital economy. When external disruptions hit — a sudden monsoon, a red-alert smog day, an unplanned curfew — they stop earning immediately. No shift, no pay. No claim form, no recourse.

Traditional insurance is designed for salaried employees. It demands paperwork, adjusters, waiting periods, and fixed monthly premiums. None of that maps to a worker who earns ₹700 on a good day and ₹0 when the city shuts down.

**GigGuard** solves exactly this gap. It is a parametric income insurance platform: when a predefined disruption condition is verified at a worker's active location, a payout fires automatically — no claim required, no adjuster involved, money in the UPI wallet within minutes.

> ⚠️ **Coverage scope:** GigGuard insures **lost income only.** Vehicle repair, health, life, and accident costs are explicitly out of scope.

---

## Our Chosen Persona

**Segment: Food Delivery Partners — Zomato & Swiggy**

**Why this segment:**
- Largest sub-category of gig workers in India (~5M active riders)
- Entirely outdoor, weather-exposed work with zero income protection
- Already operate on weekly payout cycles (Zomato Weekly Settlement, Swiggy Weekly)
- High smartphone penetration and existing app-comfort makes mobile onboarding viable
- Weather disruptions are frequent, hyperlocal, and independently verifiable — ideal for parametric triggers

---

## Persona-Based Scenarios & Application Workflow

### Persona 1 — Ravi, Full-Time Food Delivery Rider (Bengaluru)

**Profile:**
- Age 28 · Delivers for Zomato · 10–12 hrs/day · Earns ₹700–950/day
- No savings buffer · Has lost 3–4 earning days per monsoon season with zero compensation
- Primary concern: sudden Bengaluru downpours that escalate to red-alert within minutes

**Scenario: Monsoon disruption payout**

- `08:30 AM` — Ravi activates his shift in the GigGuard app. Weekly premium of ₹49 was auto-debited on Monday. Coverage is live.
- `06:45 PM` — IMD issues red-alert for Bengaluru South (Ravi's active zone). Rainfall exceeds 40mm/hr — parametric trigger condition met.
- `06:46 PM` — GigGuard trigger engine detects event and matches Ravi's live location to zone. Multi-signal verification fires: GPS · cell towers · accelerometer · barometer. Composite fraud score: 0.09 → AUTO-APPROVE path.
- `06:49 PM` — ₹250 income disruption payout sent to Ravi's UPI ID. Push notification: *"Storm payout of ₹250 sent. Stay safe, Ravi."*
- **Total elapsed time: 3 minutes 20 seconds. Ravi filed nothing.**

---

### Persona 2 — Sunita, Part-Time Delivery Partner (Pune)

**Profile:**
- Age 34 · Swiggy partner · Works 8 AM–1 PM only · Earns ₹350–450/shift
- Worried about paying for insurance on days she doesn't work
- Lives in a low-connectivity area — GPS drops near her housing complex

**Scenario: Heatwave payout with connectivity grace**

- `08:00 AM` — Sunita activates her morning shift. Part-time tier: ₹29/week premium.
- `11:15 AM` — IMD heat index crosses 43°C in Pune Central — trigger condition met. Sunita is active and in the affected zone.
- `11:16 AM` — Verification runs. GPS signal weak near underpass — location confidence: LOW. System detects heatwave advisory is active → coherence band widened. Cell tower triangulation independently confirms zone. Score: 0.41 → SOFT FLAG.
- `11:18 AM` — Human reviewer notified. Confirms via cell data within 35 minutes. ₹150 heat disruption payout released. No fraud mark on profile.
- `01:00 PM` — Sunita ends shift. Coverage pauses. No charge for the afternoon.

---

### Persona 3 — Imran, Veteran Rider with High Trust Score (Delhi NCR)

**Profile:**
- Age 38 · Zomato partner for 3 years · 200+ clean claim history
- Regularly rides through dense winter fog and smog advisories on NH-48
- Concerned about being flagged unfairly — he's been through the system before

**Scenario: Fog disruption, high-trust fast lane**

- `07:00 AM` — Imran activates shift. Trust score: 0.91 (3 years, 200+ clean claims). Anomaly band is widened — Imran gets benefit-of-the-doubt threshold.
- `07:30 AM` — IMD Dense Fog advisory: visibility <50m on NH-48 corridor. Trigger condition met. Imran's location verified. Fraud score: 0.06 (well within widened band) → AUTO-APPROVE.
- `07:32 AM` — ₹200 fog disruption payout sent. Imran never touched the app.

---

### Core Application Workflow

**Step 1 — Worker mobile app**
The worker onboards, builds a risk profile, and activates their shift. The app pings location every 5 minutes during active shifts only — no background tracking when the shift is off.

**Step 2 — Trigger engine**
The engine continuously cross-references the worker's live location against real-time feeds from IMD and OpenWeatherMap. A trigger fires only when both sources independently confirm a qualifying disruption condition in the worker's exact micro-zone.

**Step 3 — Multi-signal verification layer**
On trigger, the system runs a composite fraud check across GPS, cell towers, accelerometer, barometer, Wi-Fi probe data, and physics plausibility. This produces a risk score between 0.0 and 1.0.

**Step 4 — Outcome routing**
- Score < 0.3 → Auto-approve: UPI payout disbursed in under 5 minutes
- Score 0.3–0.7 → Soft flag: Human reviewer resolves within 2-hour SLA, payout held not cancelled
- Score > 0.7 → Hard block: Case escalated to fraud team, appeal path available

**Step 5 — Feedback loop**
All outcomes — approvals, reversals, and blocks — feed back into the worker's trust score and the platform's ML baseline, continuously improving accuracy over time.

---

## Weekly Premium Model, Parametric Triggers & Platform Choice

### Weekly Premium Model

GigGuard uses a **usage-gated micro-premium** structure built around how food delivery workers actually earn — variable hours, weekly settlements, no fixed monthly income.

| Tier | Weekly Hours | Weekly Premium | Max Weekly Payout | Coverage Window |
|---|---|---|---|---|
| Full-time | > 30 hrs | ₹49 | ₹1,200 | All active shift hours |
| Part-time | 10–30 hrs | ₹29 | ₹600 | Active shift hours only |
| Occasional | < 10 hrs | ₹15 | ₹300 | Active shift hours only |

**How it works:**
- Premium auto-debits every **Monday morning** via UPI Autopay or Razorpay recurring mandate
- Coverage is **shift-activated, not always-on** — a worker who doesn't tap "Start Shift" is not tracked and not covered that day, preserving privacy and battery
- A **3-day grace period** applies for failed auto-debits before coverage lapses, preventing gaps during end-of-month cash crunches
- **Platform subsidy pathway:** Zomato/Swiggy can enrol and subsidise premiums for their active partners as a retention benefit, reducing worker out-of-pocket cost to ₹0 via API integration at onboarding
- Payouts count against the weekly cap — once reached, no further payouts fire until the next Monday reset

---

### Parametric Triggers

All triggers are **objective, dual-source verified, and income-loss specific.** No human discretion in the trigger decision.

| Disruption Type | Trigger Condition | Payout Amount |
|---|---|---|
| **Heavy rain** | IMD red/orange alert + rainfall ≥ 35mm/hr at worker's active zone | ₹200 – ₹300 |
| **Extreme heat** | Heat index ≥ 42°C sustained for ≥ 2 hrs during active shift | ₹150 |
| **Dense fog** | IMD visibility advisory < 50m on worker's active road corridor | ₹200 |
| **Severe air quality** | AQI > 400 (Severe+) in worker's active PIN code zone | ₹100 |
| **Cyclone warning** | IMD cyclone alert within 100km of worker's registered city | ₹500 flat |
| **Unplanned curfew / strike** | Government-issued curfew order OR verified platform-wide zone closure | ₹250 |

**Dual-source confirmation rule:** Both IMD (primary) and OpenWeatherMap (secondary) must confirm the trigger condition independently. This prevents a single bad weather feed from firing mass payouts. For social disruptions, confirmation requires an official government notification API signal plus a platform partner zone-closure signal.

> **What is never covered:** Vehicle breakdown, health issues, accidents, traffic delays, personal emergencies. GigGuard insures the external condition causing income loss — not any downstream consequence.

---

### Platform Choice: Mobile (Android-First)

| Factor | Decision |
|---|---|
| **Device reality** | 94%+ of food delivery workers in India use Android as their only device |
| **Core UX actions** | Shift activation, location tracking, UPI payout — all native to mobile |
| **Fraud defense** | Android native APIs (`isFromMockProvider()`, accelerometer, barometer) are critical to our verification layer |
| **Notification model** | Push alerts for payout confirmation and weather warnings require a mobile client |
| **Web dashboard** | Exists for fraud ops teams and platform partners to review flagged claims and view analytics — not for workers |

A web interface for workers would add friction with no benefit. The product lives on the phone because the worker lives on the phone.

---

## AI/ML Integration Plan

### 1. Dynamic Premium Calculation

**Model:** Gradient-boosted regression (XGBoost)

**Inputs:**
- Worker's historical active hours per week
- Zone-level weather risk score (rolling 90-day disruption frequency)
- Seasonal risk index (monsoon season = elevated)
- City tier and microzone (coastal vs. inland, low-lying flood zone vs. elevated)
- Platform tenure and rating (proxy for reliable location data)
- Prior claim history

**Output:** A personalised weekly premium within the tier bands defined above. Workers in chronically high-risk zones (Mumbai coastal areas during June–September) price toward the upper band; long-tenure workers in low-disruption zones toward the lower band.

**Cold-start handling:** New workers are assigned city-average risk scores for their zone until 4 weeks of shift data accumulates. No worker is penalised with a high premium during onboarding.

---

### 2. Location Verification & Anomaly Scoring

**Model:** Isolation Forest (unsupervised anomaly detection) + deterministic physics rules

**Inputs per claim event:**
- GPS coordinates + confidence interval
- Accelerometer / gyroscope readings (motion coherence)
- Barometric pressure vs. weather API reading at claimed location
- Cell tower triangulation delta
- Wi-Fi SSID probe fingerprint
- `isFromMockProvider()` Android flag
- Speed and altitude transition plausibility
- Worker's historical location patterns for this zone

**Output:** Composite risk score 0.0–1.0 routing to auto-approve / soft-flag / hard-block.

---

### 3. Fraud Ring / Syndicate Detection

**Model:** Temporal Graph Neural Network (PyTorch Geometric)

**Inputs:**
- Pairwise claim submission timestamps across all active workers
- GPS proximity clusters (workers claiming within 50m of each other)
- Device model and OS version homogeneity within a claim cluster
- IP subnet overlap across simultaneous claims
- Encrypted messaging app network activity spike (metadata only, not content)

**Output:** Ring confidence score per cluster. High-confidence clusters trigger liquidity hold and ops escalation before payout execution. The ring detector runs as a streaming job — evaluating incoming claims in real time against the current active-claim graph, not in batch after the fact.

---

### 4. Weather-Location Correlation Engine

**Model:** Geospatial interpolation (Kriging / inverse distance weighting) over IMD grid data

**Inputs:**
- IMD real-time weather feed (rain gauge network, radar composite)
- OpenWeatherMap hyperlocal data
- Worker GPS ping (every 5 minutes during active shift)

**Output:** Per-worker micro-zone weather severity score, updated every 5 minutes. A worker 800m outside the red-alert boundary does not receive a payout — the engine is precise to the worker's actual location, not their city or PIN code. This geographic precision is what separates GigGuard from a crude city-level trigger system.

---

### 5. Trust Score & Adaptive Thresholds

**Model:** Bayesian update on worker-level prior

**Inputs:** Verified claim history, clean verification streak, platform tenure, partner rating, appeal outcomes.

**Output:** Per-worker trust score (0.0–1.0) that widens the anomaly tolerance band for workers with a strong clean history, and tightens it for accounts with prior flags or new registrations. The system becomes more frictionless for honest long-term workers — not uniformly paranoid for everyone forever. A week-old account with no history gets a tighter threshold by default; Ravi with 3 years of clean claims almost never sees a soft-flag.

---

## Tech Stack & Development Plan

### Tech Stack

| Layer | Technology | Rationale |
|---|---|---|
| **Mobile app** | React Native (Android-first) | Cross-platform base; native module access for sensors and location APIs |
| **Backend API** | Node.js + Express | Fast REST API for mobile; event-driven architecture suits real-time trigger model |
| **ML services** | Python · FastAPI · XGBoost · PyTorch Geometric · scikit-learn | Python ML ecosystem; FastAPI for low-latency scoring endpoints |
| **Database** | PostgreSQL (transactional) + Redis (real-time location cache) | Relational for claims/policies; Redis for hot location state during active shifts |
| **Weather APIs** | IMD Data Portal · OpenWeatherMap · AQICN | IMD for official trigger authority; OWM for hyperlocal secondary confirmation |
| **Payments** | Razorpay UPI Autopay (premium debit) + Razorpay Payout API (disbursement) | Full UPI stack in one provider; sandbox available for Phase 1–2 |
| **Location** | Google Maps Platform + Android native location APIs | Geofencing, reverse geocoding, and native sensor access |
| **Hosting** | AWS (EC2 · RDS · Lambda for trigger engine · SQS for payout queue) | Lambda suits event-driven trigger model; SQS ensures no payout is dropped |
| **Monitoring** | Datadog (infrastructure) · Sentry (app errors) | Standard observability stack |

---

### Development Roadmap

#### ✅ Phase 1 — Ideation & Foundation 
- [x] Persona research and disruption mapping
- [x] Full README strategy document
- [x] Premium model and trigger logic design
- [x] Anti-spoofing architecture design
- [x] Phase 1 prototype: app shell + trigger stub + risk scorer demo
- [x] 2-minute strategy video

#### 🔲 Phase 2 — Core Build 
- [ ] Worker onboarding flow (KYC-lite + UPI mandate setup)
- [ ] Shift activation / deactivation with background location tracking
- [ ] Trigger engine: IMD + OWM integration + zone-matching logic
- [ ] Basic location verification (GPS + cell tower delta check)
- [ ] UPI payout disbursement (Razorpay sandbox)
- [ ] PostgreSQL schema: workers · shifts · claims · payouts · trust_scores

#### 🔲 Phase 3 — Intelligence Layer 
- [ ] Isolation Forest anomaly scorer on live claim submissions
- [ ] Temporal GNN ring detector (streaming, not batch)
- [ ] XGBoost dynamic premium model (trained on synthetic + IMD historical data)
- [ ] Trust score system with adaptive threshold adjustment
- [ ] Fraud ops web dashboard: flagged claim queue + signal breakdown

#### 🔲 Phase 4 — Polish & Demo 
- [ ] End-to-end scenario testing: all 3 personas + simulated fraud ring
- [ ] False positive tuning across all signal weights
- [ ] Load testing: 10,000 concurrent active workers on trigger engine
- [ ] Analytics dashboard: payout volume · fraud catch rate · avg verification time
- [ ] Demo-ready build with full persona walkthroughs

---

## Adversarial Defense & Anti-Spoofing Strategy

### The Threat Model

A coordinated group of workers uses GPS-spoofing apps (e.g., Fake GPS, mock location providers) while staying home, tricking the platform into paying out for weather events they never experienced. The exploit has three characteristics that make it detectable: the GPS signal is *digitally injected*, the device *stops moving*, and the fraud is *coordinated across multiple accounts simultaneously*.

---

### 1. Differentiation — Genuine Worker vs. Bad Actor

Simple GPS is trivially fakeable. Our defense is **sensor fusion** — requiring physical consistency across signals that a spoofing app cannot all fake at once.

| Signal | Genuine Worker | Spoofed Device |
|---|---|---|
| **Accelerometer / gyroscope** | Micro-vibrations: wind, movement, shelter-seeking | Near-zero motion — phone sitting still at home |
| **Barometric pressure** | Matches weather API reading at claimed location (±5 hPa) | Home air pressure diverges from claimed storm zone |
| **Cell tower triangulation** | Corroborates GPS zone independently | Towers place device in home neighbourhood, not the storm zone |
| **Wi-Fi probe fingerprint** | Commercial / roadside SSIDs visible | Domestic SSIDs — inconsistent with a street claim |
| **Physics plausibility** | Speed and altitude transitions are physically possible | GPS track shows impossible jumps before claim window |

Each signal alone is soft. All five fused into a **composite risk score (0.0–1.0)** create a classifier that is extremely difficult to defeat simultaneously. A spoofing app overrides the GPS chipset output — it cannot also fake the accelerometer, rewrite the barometer, redirect SIM tower pings, mask home Wi-Fi, and produce a credible motion history at the same time.

---

### 2. The Data — Detecting a Coordinated Ring

| Signal | What It Reveals |
|---|---|
| **Claim submission timestamps** | 500 workers filing within a 90-second window is statistically impossible without coordination. Inter-claim time deltas monitored in real time across the full portfolio. |
| **Device network metadata** | Spike in encrypted messaging app traffic immediately before mass claims indicates a broadcast coordination trigger. Network pattern observed — not message content. |
| **Device model homogeneity** | Fraud rings bulk-provision cheap Android devices. 80%+ of a suspicious cluster sharing the same make/model/OS is a significant statistical signal. |
| **Historical route graphs** | GNN flags workers claiming to be in a zone they have never entered in 6 months of verified location history. |
| **Pairwise GPS overlap** | Workers A and B claiming locations within 50m of each other in the same 3-minute window — pattern holding across 20+ pairs — fires the ring detector. |
| **IP address clusters** | Claims resolving to the same home ISP subnet contradict being dispersed across a large storm zone. |
| **`isFromMockProvider()` flag** | Android's native mock location flag checked on every GPS ping. Suppressed by advanced apps — defeated by sensor incoherence above. |

**Ring detection:** Temporal graph clustering model. Nodes = workers, edges weighted by co-occurring suspicious signals. Dense clusters with tight time spread trigger an automatic **liquidity hold + ops escalation** before disbursement.

---

### 3. UX Balance — Protecting Honest Workers

> **Core principle: friction scales with risk score, not with suspicion.**

**🟢 Score < 0.3 — Auto-Approve**
Payout in under 5 minutes via UPI. No worker interaction required. This is the experience for the large majority of legitimate claims.

**🟡 Score 0.3–0.7 — Soft Flag → Human Review (2-hr SLA)**
Payout held, not cancelled. Worker notified neutrally: *"We're verifying your claim — you'll hear back within 2 hours."* If cleared, payout releases retroactively with no fraud mark on the profile. The coherence band is automatically widened during confirmed red-alert events to account for GPS degradation in heavy rain and underground areas.

**🔴 Score > 0.7 — Hard Block**
Payout held, case escalated to fraud team with full signal evidence. Worker notified: *"We've flagged an issue with your claim for review. Our team will contact you within 24 hours."* Appeal path with geotagged photo/video upload available.

| False Positive Scenario | Response |
|---|---|
| Worker cleared after hard block | Held amount + **5% inconvenience credit** released automatically |
| Signal generating high false positive rate | That signal's weight **auto-downregulated** via ML feedback loop |
| Long-tenure worker with clean history | Wider anomaly band — 18+ months / 200+ clean claims earns meaningful leniency |

---

### Architectural Summary

- **GPS alone** — trivially spoofable
- **GPS + device sensors** — hard to fake
- **GPS + sensors + network triangulation** — very hard to fake
- **GPS + sensors + network + behavioral history** — extremely hard to fake
- **All of the above + temporal ring detection** — requires defeating a live streaming system simultaneously

The honest worker never needs to think about any of this. The syndicate cannot beat all layers at once.

---

## Phase 1 Prototype Scope

| Feature |  Notes |
|---|---|---|
| Worker app shell |  Shift activation toggle, premium status, mock payout history |
| Trigger engine stub |  Hardcoded weather event fires against a test worker's pinned location |
| Risk scorer demo | Synthetic claim inputs → composite score → routing decision displayed |
| Payout confirmation screen |  UPI mock flow showing ₹250 weather disruption notification |
| Live weather API integration |  IMD + OWM live feeds |
| Real UPI disbursement |  Razorpay sandbox |
| ML anomaly scorer |  Isolation Forest on live data |
| Ring detector |  Temporal GNN streaming |

---

## Repository & Demo

| Resource | Link |
|---|---|
| **GitHub Repository** | https://github.com/ayeshakhurana/GigGuard |
