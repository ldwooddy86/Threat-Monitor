# DalesOracle v2 — using the skill on any country

DalesOracle turns one sentence — *"run /dalesoracle on Iran"* — into an open-source
intelligence product on that country's military posture: a self-contained HTML dashboard
(15 tabs, IC-grade tradecraft, every number sourced and dated) and, optionally, a hardened
Chrome extension that adds live public channel lanes, a movement-language scanner and a
public-ADS-B Track Watch. This guide is for the person running the skill. `SKILL.md` is the
build procedure Claude follows; `assets/extension/README.md` documents the extension itself;
`references/` holds the schema, tradecraft standards, research playbook and ADS-B codes.

Everything the skill produces is public reporting. Its value is currency and synthesis — a
sourced, graded, honest picture on the day you ask for it — not secrets, and never targeting.

---

## 1. Invoking it

Any of these triggers the skill:

| you say | what you get |
|---|---|
| `Run /dalesoracle on Iran` | Full-spectrum build: dashboard + extension, protective layer on, escalation model where a conflict pathway is the question |
| `DalesOracle on Nigeria, dashboard only` | Dashboard, no extension zip |
| `A DalesOracle on Pakistan and India — separate dashboards for each` | Two independent builds (each gets its own research pass, data file and outputs) |
| `Refresh the China DalesOracle` | Re-research on today's date; the BLUF's *what changed* strip lists what moved since the previous edition |
| `DalesOracle on Russia, naval and strategic forces only` | Narrowed coverage — fewer matrix domains and systems groups; the schema supports it |
| `DalesOracle on Kenya, no protective layer` | Military-only 11-tab build (the four protective tabs hide) |
| `DalesOracle on South Korea` | Ally / status-quo subject — the product reframes from "threat monitor" to "posture and strategic trajectory" (see §3) |

Claude confirms four scoping choices before it starts (and states its assumptions if you are
not around to answer): the **country / force** (e.g. Iran = IRGC + Artesh), the **coverage**
(default full-spectrum), whether the **protective layer** is in scope (default yes), whether an
**escalation model** is warranted (yes where a conflict pathway is the analytic question —
Taiwan, Korea, the Gulf, Kashmir), and whether you want the **extension** as well as the
dashboard (default: both).

A full build is a research-heavy task: expect dozens of web searches and fetches before any
file is written, because the skill refuses to carry numbers forward from a prior build or from
memory. That is the point.

---

## 2. What a build does, in plain language

1. **Scope** the subject and coverage.
2. **Research on the build date** — reference baselines (IISS Military Balance, SIPRI, FAS
   Nuclear Notebook, the relevant DoD / allied assessment), then the perishables that age in
   weeks: commanders and purges, the latest budget, the newest exercise, test, deployment or
   incident, sanctions and summits; then each domain; then the protective layer (terrorism
   index, actors, incidents, infrastructure, data centers); then the live-layer checks.
3. **Populate `data.js`** from a fresh scaffold — never by editing another country's content.
4. **Verify the live layer**: every Telegram handle is fetched to confirm a real public post
   stream (contact-only pages are rejected); ADS-B designators are taken from the verified list.
5. **Red-team, then validate**: name the strongest evidence *against* the headline, confirm
   the ACH board carries genuine disconfirming evidence, reconcile the numbers across sections,
   then run the validator — which refuses to build on any error.
6. **Build** the self-contained dashboard; **package** the extension; **render-check** every
   tab in headless Chromium, in preview mode and in a simulated extension mode.
7. **Deliver**: dashboard first, extension second, judgment calls named.

---

## 3. Country archetypes — how the product reframes itself

The engine is country-agnostic, but the *analytic question* is not. These are the framings
that have proved right in practice; Claude picks one and says which.

### Peer / nuclear adversary with a defined contingency (China, Russia)
The ACH question is what the observed pattern of buildup, tempo and leadership change means
for the contingency (Taiwan, NATO's eastern flank). The escalation model is central. Warhead
custody, missile-force generation and submarine alert state are the `unseen` rows that drive
the blind fraction. Track Watch is the **allied ISR mirror** — the P-8s, RC-135s, RQ-4s,
U-2s, AEW and tanker bridges that collect against the subject — because the subject's own
aircraft fly with ADS-B off. Telegram lanes: rich for Russia (milbloggers, state channels with
public streams); essentially none official for China (aggregators and a Russian milblogger's
Asia section carry the load, and the dashboard says so).

### Nuclear regional power in a live rivalry (India, Pakistan, Israel, Iran, North Korea)
The ACH question is usually crisis pathway and escalation control: post-war posture
(India–Pakistan after May 2025), a rebuild under strike (Iran's missile and enrichment
recovery), a multi-front strain (Israel), a treaty-less arsenal (North Korea). FAS Nuclear
Notebook figures are hedged with a range (e.g. DPRK "~50, 45–100+"). Track Watch tailors to
the theatre: Cobra Ball and WC-135 for missile-test and nuclear-event collection over the East
Sea; the Hormuz / Eastern Mediterranean ISR mirror for Iran and Israel; Erieye and allied AEW
for South Asia. Scanner dictionaries carry the local languages (Urdu, Hindi, Farsi, Hebrew,
Korean) in native script and romanised form.

### Ally / status-quo defender (South Korea, Japan, Taiwan, the United States)
A "threat monitor" framing is wrong here and the skill knows it. The product becomes a
**posture and strategic-trajectory monitor**: the ACH weighs alliance-embedded hedging against
strategic-autonomy drift against domestic signalling against deterrence-stability erosion; the
escalation model covers managed deterrence, adversary provocation, alliance rupture and
inadvertent escalation. Track Watch watches the subject's *own* strategic and ISR fleet (for the
US: E-4B/E-6B nuclear C2, the tanker bridge) plus the adversary-facing mirror. The protective
layer often matters more than the order of battle.

### Internal-security-dominated state (Nigeria, Pakistan's western provinces, the Sahel)
The matrix domains become insurgency theatres and force-generation problems (ISWAP / Boko
Haram, banditry, separatism, coup-belt civil-military relations, command reform, corruption).
The protective layer is the centre of gravity — actors, target classes, infrastructure and
regional advisories carry the real threat picture — and the ACH tends toward "metastasis vs
stalemate vs rollback". Official casualty claims are flagged contested throughout. Track Watch
is the external-intervention mirror (MQ-9, P-8, RC-135, tankers over the relevant basin).

### Global power with a worldwide footprint (the United States)
Posture is read by theatre and by the strategic-C2 signature: continuity-of-government and
nuclear-command aircraft, bomber task forces, carrier surges, the tanker bridge. Budgets are
read against the fiscal topline and the arms-control state (treaty lapses reprice everything).

---

## 4. Quick notes from previous builds

These are *framing* notes from builds already run on this engine — useful as starting points,
not as current facts. Every build re-researches on its own date.

| country | subject as scoped | framing that worked | Track Watch mirror & sector | scanner languages | Telegram lanes |
|---|---|---|---|---|---|
| China | PLA (all services) | Buildup + purge + coercion pivot to the sea; Taiwan escalation model; Japan front as second axis | P-8 / RC-135+WC-135 / RQ-4 (crit) / U-2 (crit) / AEW / tankers over a Taiwan-centred 220 nm sector | EN + 中文 (romanised) | No official public streams; aggregators + Rybar's Asia section (verified) |
| Russia | Armed Forces / strategic forces (see also the RUSNuke skill) | Nuclear posture, exercises, Belarus deployments, arms-control status | Allied ISR over the Baltic / Black Sea approaches | EN + Русский | Rich: milbloggers and state channels with public streams |
| Iran | IRGC + Artesh | Rebuild under strike; enrichment blackout; Hormuz | Allied ISR mirror over Hormuz / the Gulf | EN + فارسی | Moderate; verify each handle |
| Israel | IDF | Multi-front strain; battle-tested missile defence; budget surge | Allied ISR mirror over the Eastern Mediterranean | EN + עברית | Moderate; verify each handle |
| North Korea | KPA + WMD enterprise | Solid ICBMs, destroyer programme, troops abroad, "two hostile states" | RC-135S Cobra Ball, WC-135 (crit), Rivet Joint, P-8, RQ-4/U-2 over an East Sea / DMZ sector | EN + 한국어 | None with confirmed public streams (KCNA-watch is web/X) — lanes OFF |
| South Korea | ROK Armed Forces | Posture & trajectory, not threat: alliance hedging vs autonomy drift; Three-Axis; demographic cliff | RC-135, WC-135 (crit), RQ-4, E-737, bombers (crit) over a DMZ / West Sea sector | EN + 한국어 | X/web-centric — lanes OFF |
| India | Armed Forces + strategic forces | Post-May-2025 posture, two-front planning, theatre-command reform | Allied / own AEW; Bay of Bengal / LAC approaches | EN + हिन्दी | X/official-site-centric — lanes OFF |
| Pakistan | Armed Forces + strategic forces | Post-war posture, Afghan-border war, TTP/BLA insurgency; strong protective layer (CPEC, GTI #1) | Erieye / allied AEW over the border belt | EN + اردو | X/official-site-centric — lanes OFF |
| Nigeria | Armed Forces + MNJTF | Internal-security build: NE / NW / Middle Belt / SE / Niger Delta theatres; US intervention; command reform | MQ-9 / P-8 / RC-135 / tankers over a Lake Chad Basin sector | EN + Hausa | OFF (unverified) |
| United States | Department of War / joint force | Strategic-C2 and theatre posture; New START lapse; Golden Dome | E-4B / E-6B (crit), bombers, tanker bridge | EN | OFF |

When a country's ecosystem has no Telegram channel with a confirmable public stream, the
skill ships the lanes OFF and says so on the Collection tab. That is the honesty rail working,
not a gap to paper over.

---

## 5. Reading the product

- **Posture gauge with a range.** The flag is the assessed level; the dashed band is the
  uncertainty range. "ELEVATED, range elevated–high" means the evidence could support either.
  The line under it says what observation would move it.
- **BLUF and Key Judgments (ICD-203).** Each judgment carries a probability band *and* a
  separate confidence: probability is how likely it is true, confidence is how good the
  evidence is. "Likely / Low confidence" is a legitimate — and common — combination. Each
  judgment names what would change it.
- **What changed.** The strip under the BLUF is the monitor's memory: what moved since the
  previous edition, tagged up / down / new / watch / resolved.
- **Capability matrix.** Fused level, trend and confidence per domain, plus which intelligence
  discipline can see it. Red circles are collection gaps — and the highest-consequence domains
  are usually the least observable.
- **Command chain.** Who holds each post today: confirmed, acting, vacant, purged, unknown.
  These are the most perishable facts in the product, so each row is sourced to the build date.
- **I&W board — two numbers.** The warning meter is computed over the rows that can be
  observed; the blind fraction is the share of consequence sitting in rows marked *unseen*.
  A quiet board with a 40 % blind fraction is not an all-clear.
- **ACH.** Hypotheses are ranked by least *weighted disconfirmation* — an inconsistency from a
  reliable, diagnostic source sinks a hypothesis harder than one from a weak, non-diagnostic
  source. The most tenable hypothesis is the one the good evidence fails to contradict, not the
  one with the most ticks.
- **Movement and Track Watch.** Vocabulary matches and public aircraft tracks are
  correlation, never intent. Absence on a technical feed is "cannot be judged" (F6), never
  evidence that nothing happened.
- **Protective tabs.** Threat levels use a five-step scale (low → critical); target *classes*
  carry precedent, risk and the protective posture typical for the class; sectors carry exposure
  and resilience with data centers spotlighted; regions carry advisory levels. Nothing below the
  region level, no facilities, no methods — by design and by validator.

---

## 6. The live layer (extension)

Install: unzip `<slug>-monitor-extension.zip`, open `chrome://extensions`, enable Developer
mode, **Load unpacked**, pick the folder, open the dashboard from the toolbar icon. Lanes and
Track Watch populate on the first refresh and then on a schedule (default 30 min). Settings
lets you toggle bundled lanes, add a public handle (labelled *unverified* until you confirm it),
change the interval, add your own Anthropic key for the optional synthesis panel, and clear the
cache. No key is needed for lanes, scanner or Track Watch.

What to expect by ecosystem: Russian and Ukrainian-war-adjacent subjects have deep Telegram
lanes; Middle-East subjects moderate; East Asian subjects almost none with public streams, so
the scanner will mostly see aggregator relays. Track Watch is strongest where allied ISR flies
with transponders on (the first island chain, the Baltic, the Gulf, the Korean East Sea) and
weakest where the subject's forces fly dark and no mirror fleet operates.

Security model in one line: `storage` + `alarms` only, three allowlisted hosts, CSP
`script-src 'self'`, every remote string rendered as text, GET-only worker, local-only storage,
synthesis only on your click with your key. The packager refuses any manifest that loosens it.

---

## 7. Refreshing and maintaining a country

Ask for a refresh monthly, or after any of: a leadership change or purge, a budget release, a
named exercise or missile test, a summit or sanctions move, a major incident, an arms-control
change. Say *"refresh the Iran DalesOracle"* — the skill re-runs the research on the new date,
carries the previous edition into the *what changed* strip, and re-validates. The validator
warns when a baseline is more than ~120 days old; treat a stale warning as a refresh request.

Running several countries side by side works — each build is independent (its own research
pass, `data.js`, dashboard and extension zip), and the engine is identical, so the products
read the same way. Ask for "separate dashboards" explicitly when you want two subjects rather
than one comparative product.

---

## 8. Power-user toolchain (inside the skill folder)

```bash
node scripts/scaffold_data.js --country "Iran" --adjective Iranian --subject "IRGC + Artesh" \
  --slug iran --flag "🇮🇷" --protective --escalation > assets/extension/data.js   # new-country skeleton
node scripts/verify_channels.js            # confirm every Telegram lane has a public stream, posts, freshness
node scripts/validate_data.js --strict     # the contract + the rails; ERRORs block the build
python scripts/build_preview.py --out-dir out      # self-contained dashboard HTML
python scripts/package_extension.py --out-dir out  # installable extension zip (refuses security regressions)
node scripts/render_check.js out/<slug>-military-posture-monitor-preview.html --ext --shots shots
python scripts/package_skill.py --out-dir dist     # re-bundle the skill (dalesoracle-v2.skill)
```

`references/SCHEMA.md` is the field-by-field data contract; `references/TRADECRAFT.md` the
analytic standards (ICD-203, Admiralty, ACH, I&W, the red-team checklist, the protective-layer
framing rules); `references/RESEARCH-PLAYBOOK.md` the search plan; `references/ADSB-TYPES.md`
the verified aircraft designators.

---

## 9. Limits and responsible use

- It aggregates public reporting with a lag. It cannot see warhead custody, munitions depth,
  submarine alert state or a leader's calculus, and it says so in every build.
- It is a strategic-warning and protective-security product, not a targeting tool. Asking for
  real-time unit locations, strike planning, facility vulnerabilities or a target map gets the
  analytic dashboard without that piece — the framing is a feature.
- Live lanes, scanner hits and synthesis output are unverified leads to corroborate, never
  facts to repeat. State channels and milbloggers publish false claims, sometimes deliberately.
- Estimates carry uncertainty; two numbers beside a figure are the spread, not a typo.
- The extension hardens itself; it does not anonymise your network. Use a dedicated profile
  and a VPN if your threat model needs it.

---

## 10. Troubleshooting

| symptom | cause / fix |
|---|---|
| Import rejected: *description must be at most 1024 characters* | The `SKILL.md` frontmatter description is over the limit; v2 ships at 986 characters — re-import the current bundle |
| Validator: *ENABLED but not verified* | A Telegram handle is on without a confirmed public stream; run `verify_channels.js`, then set `verified:true` + `verifiedOn` or `enabled:false` |
| Validator: *no matcher for type key* | A `trackWatch.match` key does not match a `types[].key` — a typo that would silently blank a card |
| Validator: *protective-layer rail* | Operational vocabulary, an address or a coordinate pair in the protective block — rewrite as a defender's measure at class level |
| Validator: *placeholder text* | A `TODO` survived from the scaffold — fill or remove it |
| *baseline looks stale* warning | `meta.compiled` is more than ~120 days old — refresh |
| Track Watch always QUIET | The subject's aircraft fly dark and no mirror fleet is in the sector; widen the sector, add the allied ISR types, or accept that absence is uninformative |
| Lanes show "no public post stream" | The handle is a contact-only page or private channel — it is not a lane |
| Dashboard opens but live layers say "install for live" | You opened the preview HTML; live layers run only in the installed extension |
