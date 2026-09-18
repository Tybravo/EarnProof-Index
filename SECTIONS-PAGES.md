# EarnProof Landing Page — Sections and Pages

This document is the content and design specification for the EarnProof public
landing page. It lists **15 items in total**:

- **12 landing page sections** (Part A) — what a first-time visitor scrolls through.
- **3 linked pages** (Part B) — deeper pages that landing sections navigate into.

It is a specification only. **No section or page code is written or proposed in
this document** — implementation follows once these highlights are reviewed and
approved.

## Scope

In scope:

- The 12 landing page sections, in scroll order.
- The 3 pages linked from those sections.
- Section and page titles, descriptions, purpose, key content, and the real
  internal links and buttons each one exposes.
- The colour and gradient system to be used, drawn only from tokens that already
  exist in this repository.

Out of scope (deliberately excluded):

- The **header navbar** and the **footer**. They are existing shared shell
  components (`components/layout/public-nav.tsx`,
  `components/layout/public-footer.tsx`) and are not counted in the 15 items.
- Any landing page markup, styling, or component code.
- Header navigation labels and footer link groups.

## Where this specification comes from

Everything below is grounded in the current repository, not invented:

| Source | What it contributed |
| --- | --- |
| `README.md` | Product positioning, the primary tagline, testnet-only posture, and the "never imply credit decisions, legal identity verification, tax certification, or loan approval" constraint. |
| `app/globals.css` | Every colour token used by the design system. |
| `public/logo.svg` | The brand mark colours (navy and teal). |
| `app/page.tsx`, `app/how-it-works/page.tsx`, `app/about/page.tsx`, `app/developers/page.tsx` | The three-pillar marketing copy blocks reused by the landing sections. |
| `data/proof-types.ts` | Proof type names, descriptions, requirements, time estimates, statuses, and supported networks. |
| `lib/faq-data.ts` | The 12 FAQ entries and their six categories. |
| `components/contact/contact-form.tsx` | Contact enquiry categories, the support address, and the honest "opens your email client" behaviour. |
| `app/issuers/page.tsx`, `app/status/page.tsx` | Real directory rows, counters, and the tracked service list. |
| `docs/frontend-architecture.md`, `scripts/route-manifest.json` | The authoritative route list used for every link in this document. |
| `components/common/external-link.tsx`, `config/app.ts` | The external link allowlist rules any outbound link must satisfy. |

## Product positioning and guardrails

Primary tagline (from `README.md`, used verbatim as the Hero headline):

```text
Prove your income, not your entire financial history.
```

Positioning statement:

```text
EarnProof is an open-source, privacy-focused income and payment verification
protocol built on Stellar.
```

Non-negotiable guardrails that every landing section must respect:

1. **Make the active Stellar network visible.** Testnet status appears in the
   Hero, the network strip, the verification section, and the issuer section.
   The reference implementation is `components/common/network-badge.tsx`.
2. **Never imply** credit decisions, legal identity verification, tax
   certification, or loan approval.
3. **Never promise mainnet.** No mainnet launch date is announced; all current
   proofs are testnet only.
4. **Hide sensitive amounts by default** and show a disclosure preview before
   proof creation.
5. **Distinguish every verification state clearly** — valid, expired, revoked,
   invalid, and unverified issuer.
6. **Never expose full wallet history** on verification views.
7. **Never request or store** secret keys, seed phrases, or signing material.
8. **Do not overstate issuer listings.** Registry and Stellar references are
   evidence, not endorsement, and do not assert live contract state.

---

## Colour system

Every colour below is copied from the existing design system. The tokens come
from `app/globals.css`; the status colours are already used across the app; the
brand colours come from `public/logo.svg`.

### Core design tokens (`app/globals.css`)

| Token | Hex value | Tailwind class already used in the app | Landing page role |
| --- | --- | --- | --- |
| `--background` | `#020617` | `bg-slate-950` | Page background, every section base. |
| `--surface` | `#0f172a` | `bg-slate-900` | Raised surfaces, gradient mid-stops, form fields. |
| `--surface-soft` | `rgba(255, 255, 255, 0.04)` | `bg-white/[0.04]` | Card, tile, and panel fill. |
| `--border-subtle` | `rgba(255, 255, 255, 0.1)` | `border-white/10` | Default card and divider border. |
| `--border-default` | `rgba(255, 255, 255, 0.15)` | `border-white/15` | Input and control border. |
| `--foreground` / `--text-primary` | `#f8fafc` | `text-white`, `slate-50` | Headings and primary text. |
| `--text-secondary` | `#cbd5e1` | `text-slate-300` | Body and description text. |
| `--text-tertiary` | `#64748b` | `text-slate-400`, `slate-500` | Meta text, captions, labels. |
| `--accent` | `#67e8f9` | `text-cyan-300`, `text-cyan-200` | Accent highlights, eyebrows, links. |
| `--accent-soft` | `rgba(103, 232, 249, 0.1)` | `bg-cyan-300/10` | Accent badge and chip fill. |
| `--accent-border` | `rgba(103, 232, 249, 0.3)` | `border-cyan-300/30` | Accent badge and chip border. |
| Focus outline | `#22d3ee` | `ring-cyan-300`, `outline-cyan-200/300` | Focus and selection ring. |
| `::selection` | `rgba(103, 232, 249, 0.24)` | — | Text selection highlight. |

### Brand mark colours (`public/logo.svg`)

| Role | Hex value | Usage on the landing page |
| --- | --- | --- |
| Shield / document navy | `#0a284a` | Deep navy gradient stop behind developer and issuer sections; large watermark shapes. |
| Page fold / checkmark teal | `#02b093` | Gradient partner for cyan in primary calls to action; verified and "settled" accents. |

### Accent support shades already in use

`text-cyan-100` `#cffafe`, `text-cyan-200` `#a5f3fc`, `bg-cyan-300/[0.06]`,
`border-cyan-300/20`, and `bg-slate-300/10` for table headers and disclosure
panels.

### Semantic status colours

These are already established in the app (issuer lists, status page, proof
cards, form validation). The landing page reuses them so verification states
look identical everywhere.

| Meaning | Colour | Hex value | Classes already used |
| --- | --- | --- | --- |
| Valid, active, verified, success | Emerald | `#6ee7b7` | `text-emerald-200/300`, `bg-emerald-300/10`, `bg-emerald-300/[0.08]`, `border-emerald-300/30` |
| Review, expired, degraded, caution | Amber | `#fcd34d` | `text-amber-100/200/300`, `bg-amber-300/10`, `border-amber-300/30` |
| Revoked, invalid, error | Rose | `#fda4af` | `text-rose-100/200`, `bg-rose-300/10`, `border-rose-300/30` |
| Inline form validation error | Red | `red-400` | `text-red-400` |

Rule: **no state may be communicated by colour alone.** Every badge pairs its
colour with a text label (as `StatusBadge` already does).

### Gradient treatment

Honest note: **the repository contains no `bg-gradient-*` utility today.** The
gradients below are therefore new compositions, but they are built *only* from
the hex values already listed above — no new colours are introduced.

| Name | Recipe (existing tokens only) | Applied to |
| --- | --- | --- |
| `hero` | `linear-gradient(135deg, #020617 0%, #0f172a 45%, rgba(103,232,249,0.14) 100%)` plus a soft radial glow of `rgba(2,176,147,0.12)` in the top-right | Sections 1 and 5 |
| `stellar-navy` | `linear-gradient(180deg, #020617 0%, rgba(10,40,74,0.65) 100%)` | Sections 8 and 9 |
| `cta-primary` | `linear-gradient(90deg, #67e8f9 0%, #02b093 100%)`, always with `text-slate-950` label text | Primary buttons in Sections 1, 11, 12 |
| `status-strip` | `linear-gradient(90deg, rgba(110,231,183,0.08) 0%, rgba(103,232,249,0.08) 100%)` | Sections 2 and 7 |
| `contact-veil` | `radial-gradient(circle at 30% 20%, rgba(2,176,147,0.15) 0%, rgba(15,23,42,0.9) 60%, #020617 100%)` | Section 12 |
| `panel-sheen` | `linear-gradient(180deg, rgba(255,255,255,0.06) 0%, rgba(255,255,255,0.02) 100%)` | Tiles and cards sitting inside a gradient section |
| `accent-rule` | `linear-gradient(90deg, rgba(103,232,249,0) 0%, rgba(103,232,249,0.3) 50%, rgba(103,232,249,0) 100%)` | Thin divider at the top of every section |

### Accessibility rules for gradient sections

These follow the existing requirements in `docs/accessibility-testing.md`:

1. Body copy on any gradient stays at `#cbd5e1` (`text-slate-300`) or brighter.
2. A gradient call to action keeps dark label text (`text-slate-950`) on the
   cyan-to-teal fill, matching the current primary button pattern.
3. Focus indicators stay cyan (`ring-cyan-300` / `outline-cyan-200`), the
   success colour in `app/globals.css`'s outline rule.
4. Contrast must be spot-checked visually on gradients, since automated contrast
   checks can miss non-solid backgrounds.
5. Gradients are decorative only. If a gradient is removed, no meaning is lost.

---

# Part A — Landing Page Sections (1–12)

These are the sections a visitor sees while scrolling the landing page at `/`,
in order. Each entry uses the same template:

- **Title** — the section heading.
- **Description** — what the section says and why it exists.
- **Purpose** — the job it does in the funnel.
- **Key content** — the blocks that make up the section.
- **Links and buttons** — every destination it exposes.
- **Gradient and colour** — its treatment, using only tokens from the colour
  system above.
- **Stellar cue** — how the section makes the blockchain feel tangible without
  overpromising.

---

## Section 1 — Hero

### Title

```text
Prove your income, not your entire financial history.
```

### Description

The Hero states the whole product in one sentence: a person can prove a
qualifying financial fact without handing over their complete transaction
history. It shows the live Stellar testnet badge, the headline claim, a short
supporting paragraph, two primary journeys (create a proof, or verify one), and
three trust chips that summarise the protocol's posture — non-custodial, open
source, and built on Stellar.

### Purpose

Answer "what is this, and is it safe?" within a few seconds, then route the
visitor into either the worker journey or the verifier journey.

### Key content

1. **Live network badge** — `Testnet` chip, using the existing
   `NetworkBadge` treatment (`border-cyan-300/50 bg-cyan-300/10 text-cyan-200`).
   Placed above the headline so the active network is visible before anything
   else, as required by `README.md`.
2. **Eyebrow** — "Open protocol", matching the existing `MarketingHero`
   component's `StatusBadge`.
3. **Headline** — the primary tagline from `README.md`, verbatim.
4. **Supporting paragraph** — from `app/page.tsx`: "Prove qualifying income
   without exposing your full financial history."
5. **Primary call to action** — gradient button, dark label text.
6. **Secondary call to action** — outlined button using `border-white/15`.
7. **Trust chip row** — three chips: "Non-custodial", "Open source",
   "Stellar testnet" (drawn from the pillars in `app/about/page.tsx`).
8. **Credential visual** — a static or lightly animated illustration of a
   credential card with a QR code and a shortened public wallet reference
   (for example `GBC4…8X2K`, the pattern already used in
   `app/issuers/veridatum-labs/page.tsx`). Amounts shown masked by default.
9. **Honest micro-disclaimer** — one line stating that EarnProof does not make
   credit decisions and is not legal identity verification, tax certification,
   or loan approval.
10. **Scroll cue** — a small downward affordance pointing to Section 2.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Create a proof" (primary) | `/proofs` | Internal |
| "Verify a proof" (secondary) | `/verify` | Internal |
| "How it works" (tertiary text link) | `/how-it-works` | Internal |

### Gradient and colour

- Background: `hero` gradient.
- Primary button: `cta-primary` fill with `text-slate-950`.
- Secondary button: transparent fill, `border-white/15`, `text-white`.
- Trust chips: `bg-white/[0.04]` fill, `border-white/10`, `text-slate-300`.
- Headline: `text-white` (`#f8fafc`).

### Stellar cue

The testnet badge sits in the headline's eye-line, and the credential visual
carries a shortened Stellar public key and a network reference line, so the
blockchain nature of the product is visible immediately rather than buried.

---

## Section 2 — Live on Stellar

### Title

```text
Live on Stellar testnet
```

### Description

A compact, honest status strip that proves the product is real and running. It
names the four pieces of infrastructure a visitor needs to trust the flow —
Stellar testnet, Horizon, the Soroban issuer registry, and the Freighter wallet
— and shows a small set of real counts pulled from existing pages. It closes
with a link to the live system status page.

### Purpose

Convert scepticism into confidence by making the network, the protocol
components, and the current operational state visible in one glance.

### Key content

1. **Network chip group** — `Stellar testnet`,
   `Horizon · horizon-testnet.stellar.org`, `Soroban registry`,
   `Freighter wallet`. The Horizon address is the documented default from
   `config/app.ts`.
2. **Metric row** — the existing `MetricGrid` treatment with real values from
   the codebase: `18` verified issuers, `16` active issuers, `7` attestation
   types (from `app/issuers/page.tsx`), `3` proof types
   (from `data/proof-types.ts`), and `5` tracked services
   (from `app/status/page.tsx`).
3. **Service legend** — the five tracked services as small labels: EarnProof
   API, Database, Stellar indexer, Smart contracts, Webhook delivery.
4. **Testnet-only statement** — an explicit line that EarnProof currently
   operates on Stellar testnet and that no mainnet date is announced.
5. **Status link** — the single call to action for this section.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "View system status" | `/status` | Internal |
| Network chips (Horizon) | `https://horizon-testnet.stellar.org` | External — see the note below |

External link note: Horizon is listed in the production content security policy
`connect-src` for documented testnet calls, but outbound **anchors** are only
allowed through `components/common/external-link.tsx`, which validates scheme
and origin against an allowlist built from `appConfig.helpUrl` and
`appConfig.stellarExplorerUrl`. If this chip becomes a clickable external link,
the Horizon origin must be added to that allowlist first. Otherwise it should
render as plain text.

### Gradient and colour

- Band background: `status-strip` gradient.
- Metric cards: `bg-white/[0.04]` fill with `border-white/10`, or `panel-sheen`
  if they sit directly on the gradient.
- Network chips: `bg-cyan-300/10`, `border-cyan-300/50`, `text-cyan-200` — the
  same accent treatment as `NetworkBadge` and `StatusBadge`.
- Live indicators: emerald `#6ee7b7` for healthy, amber `#fcd34d` for degraded
  or unknown, matching `app/status/page.tsx`.
- Metric numbers: `text-white`, labels `text-slate-300`.

### Stellar cue

The strip is the section that turns "built on Stellar" from a slogan into
concrete infrastructure names — a named network, a named Horizon host, a named
contract platform, and a named wallet — each with a visible health state.

---

## Section 3 — The Problem

### Title

```text
Sharing one payslip reveals everything you didn't ask to share
```

### Description

A side-by-side contrast between what a conventional proof of income exposes
(wallet history, counterparties, balances, unrelated transactions) and what an
EarnProof claim exposes (one attested fact, such as "income met or exceeded a
threshold"). This is the emotional and rational core of the privacy pitch.

### Purpose

Make the cost of over-disclosure obvious, so the rest of the page reads as a
solution to a problem the visitor now recognises.

### Key content

1. **Left panel — "A bank statement or payslip"** — a list of what leaks:
   exact balances, every counterparty, unrelated transactions, spending
   patterns, and full wallet history.
2. **Right panel — "An EarnProof claim"** — a short list of what is actually
   revealed: the attested claim only, the issuer, the expiry, and the proof
   status. Amounts are shown masked by default, mirroring the "hide sensitive
   amounts by default" requirement in `README.md`.
3. **Contrast callout** — one sentence summarising the principle: reveal the
   minimum necessary fact, nothing more. This connects directly to the
   "Selective disclosure" pillar in `app/page.tsx`.
4. **Exclusion note** — a line stating that exclusions are reviewed before they
   contribute to a proof, referencing the "Choose qualifying payments" step in
   `app/how-it-works/page.tsx`.
5. **Privacy link** — routes to the full privacy policy.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Read the privacy policy" | `/privacy` | Internal |
| "See how selective disclosure works" | `/proof-types` | Internal |

### Gradient and colour

- Base background: `--background` `#020617`, no gradient, so the contrast reads
  cleanly.
- Left panel (the risk side): `bg-rose-300/10` fill with `border-rose-300/30`
  border, echoing the app's existing error treatment.
- Right panel (the safe side): `bg-emerald-300/[0.08]` fill with
  `border-emerald-300/30`, echoing the app's existing success treatment.
- Blurred or masked values: `text-slate-400` with a masked placeholder.
- Divider between the two panels: `accent-rule` gradient.

### Stellar cue

The right-hand panel shows a proof reference as a shortened on-chain-style
identifier, so the safe side still reads as verifiable cryptography rather than
a promise from a company.

---

## Section 4 — How It Works

### Title

```text
Three steps from wallet payments to a shareable credential
```

### Description

The protocol flow, told in the same three steps the product actually
implements: connect safely, choose qualifying payments, and share only the
claim. Each step carries a privacy annotation so the visitor understands what
does *and does not* happen at that moment. The section ends by handing off to
the full walkthrough page.

### Purpose

Remove "how does this actually work?" friction before the visitor is asked to
connect a wallet.

### Key content

1. **Step 1 — Connect safely.** Approve a readable wallet challenge. EarnProof
   never asks for a seed phrase or custody permission.
2. **Step 2 — Choose qualifying payments.** Select only eligible records and
   review exclusions before they contribute to a proof.
3. **Step 3 — Share only the claim.** Preview every disclosed field, keep exact
   amounts hidden, and confirm the claim before sharing.

   All three step titles and descriptions are taken verbatim from
   `app/how-it-works/page.tsx`, so the landing page and the product page agree.
4. **Per-step privacy annotation** — a small note under each step stating what
   is *not* accessed at that stage (for example: "No key material leaves your
   device").
5. **Connector line** — a vertical or horizontal progress line joining the three
   steps, with the accent gradient.
6. **Handoff link** — the full walkthrough.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "See the full walkthrough" | `/how-it-works` | Internal |
| "Start with a proof" | `/proofs` | Internal |

### Gradient and colour

- Section background: `#020617`, flat.
- Step tiles: `panel-sheen` gradient over `bg-white/[0.04]`, `border-white/10`.
- Step numbers: cyan `#67e8f9` on `bg-cyan-300/10` circles with
  `border-cyan-300/50`.
- Connector line: `accent-rule` gradient.
- Privacy annotation text: `text-slate-400`, sitting below `text-slate-300`
  body copy so it reads as secondary.

### Stellar cue

Step 1 shows the wallet challenge text as a signed-message preview, and step 3
shows a credential with an issuer signature and a network reference, making the
signing and verification model visible instead of abstract.

---

## Section 5 — Proof Types and Capabilities

### Title

```text
What you can prove today, and what's next
```

### Description

A catalogue of the supported proof types with their real availability status,
requirements, estimated time, and network. Only Minimum Income is available
now; Recurring Income and Payment Receipt are explicitly marked as planned. The
section is deliberately honest about what does not exist yet.

### Purpose

Let the visitor self-qualify — "is the thing I need to prove available?" — and
route the eligible ones into proof creation.

### Key content

1. **Minimum Income** — status `available`. Description: prove income meets or
   exceeds a threshold without revealing exact earnings or transaction details.
   Requirements: a Stellar testnet wallet with payment history, qualifying
   payments within a specified period, and a minimum threshold amount.
   Estimated time: 5–10 minutes. Networks: testnet.
2. **Recurring Income** — status `planned`. Demonstrate consistent income
   patterns over multiple periods while maintaining payment privacy.
   Estimated time: coming soon.
3. **Payment Receipt** — status `planned`. Verify specific payment transactions
   without exposing wallet balances or other financial data.
   Estimated time: coming soon.

   All values come from `data/proof-types.ts`, so the landing page cannot drift
   from the product.
4. **Status badge per card** — `available` renders as success (emerald),
   `planned` renders as warning (amber), using the existing `StatusBadge`
   `tone` prop.
5. **Card footer action** — available types get an active button; planned types
   get a disabled "Coming soon" button, matching the existing proof type card
   behaviour in `app/proof-types/page.tsx`.
6. **Catalogue link** — the full proof type browser.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Browse all proof types" | `/proof-types` | Internal |
| "Create a proof" (on the available card) | `/proofs` | Internal |
| Minimum Income detail link | `/proof-types/minimum-income` | Internal |
| "Coming soon" (planned cards) | none, disabled | Inert by design |

### Gradient and colour

- Background: soft `hero` gradient, lighter than Section 1 so it does not
  compete with the Hero.
- Cards: `panel-sheen` over `bg-white/[0.04]`, `border-white/10`.
- Available badge: `bg-emerald-300/10`, `border-emerald-300/30`,
  `text-emerald-200`.
- Planned badge: `bg-amber-300/10`, `border-amber-300/30`, `text-amber-200`.
- Disabled button: `border-slate-400/30 bg-slate-400/10 text-slate-400` with
  `cursor-not-allowed`, matching the existing pattern.
- Active button: `cta-primary`.

### Stellar cue

Each card names its supported network ("testnet"), and the available card notes
that the eligibility check runs against Stellar payment history, so the
blockchain dependency is stated as a requirement rather than decoration.

---

## Section 6 — Selective Disclosure and Privacy Controls

### Title

```text
You approve every field before anything is shared
```

### Description

A walkthrough of the disclosure preview: the visitor sees, field by field,
exactly what a verifier will receive. Amounts are hidden by default, excluded
payments are listed, and nothing is shared until the visitor confirms. This
section turns the abstract promise of privacy into a visible, reviewable
control.

### Purpose

Answer the visitor's sharpest question — "what exactly will they see about me?"
— with a concrete answer rather than a policy link.

### Key content

1. **Disclosure preview panel** — a small table of fields with a visible
   included/hidden state per row: claim type, threshold satisfied,
   issuer, period, expiry, and proof status. Exact amounts render as masked
   placeholders (`••••`) rather than numbers.
2. **Hidden-by-default note** — an explicit statement that sensitive amounts are
   hidden by default, mirroring the requirement in `README.md`.
3. **Exclusion list** — the payments that were deliberately left out and why,
   referencing the exclusion-review step in
   `components/proofs/privacy-controls.tsx`.
4. **Confirm step** — a representation of the confirmation action that must be
   taken before a claim is shared.
5. **No-history statement** — a line stating that no wallet history is exposed on
   verification views, and that raw credentials, IP addresses, and wallet
   activity are not stored (from `lib/faq-data.ts`).
6. **Disclosure-style closing panel** — the same visual pattern used on the
   privacy page's "Disclosure summary" block.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Read the privacy policy" | `/privacy` | Internal |
| "See proof types" | `/proof-types` | Internal |
| "Frequently asked questions" | `/faq` | Internal |

### Gradient and colour

- Background: `#020617`, flat.
- Preview panel: `bg-white/[0.04]` with `border-white/10`, or the
  `bg-slate-300/10` treatment used for the existing disclosure summary blocks.
- Included field marker: emerald `#6ee7b7`.
- Hidden field marker: `text-slate-400` with a masked value.
- Eyebrow label ("Disclosure preview"): `text-cyan-200` with uppercase
  tracking, matching the existing pattern.
- Panel edge: `border-white/15`, the default border token.

### Stellar cue

The preview shows a proof reference and an issuer signature line, so the visitor
understands that what they are approving is a signed cryptographic claim, not a
copy of their financial records.

---

## Section 7 — Verify a Proof

### Title

```text
Verification that anyone can repeat
```

### Description

The verifier-facing counterpart to the worker flow. It presents the three ways a
proof can be verified — by proof ID, by uploading a credential, or by scanning a
QR code — and explains what each outcome means. It also publishes the full
status legend so a verifier knows what "expired", "revoked", and "unverified
issuer" actually mean before they see one.

### Purpose

Convince verifiers and employers that a claim can be checked independently and
that the result is unambiguous.

### Key content

1. **Three verification entry points** — Proof ID entry, credential upload, and
   QR scan, matching the three real routes.
2. **Status legend** — four outcomes with their colours and one-line meanings:
   - Valid / active — emerald `#6ee7b7`
   - Expired — amber `#fcd34d`
   - Revoked — rose `#fda4af`
   - Invalid or unverified issuer — amber `#fcd34d`
3. **What a verifier checks** — a short list: proof signature, issuer trust,
   expiry, and revocation state. Verbatim intent from `lib/faq-data.ts`:
   "The verifier checks the proof signature, issuer trust, and expiry on-chain
   via Stellar references."
4. **No-history reassurance** — a statement that verification views show only
   intentionally disclosed claim data.
5. **Issuer warning state** — a small sample of the unverified-issuer warning, as
   surfaced by the product.
6. **Portal link** — the primary call to action into the verification flow.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Verify a proof" (primary) | `/verify` | Internal |
| "Upload a credential" | `/verify/credential` | Internal |
| "Scan a QR code" | `/verify/scan` | Internal |
| Issuer trust explainer | `/issuers` | Internal |

### Gradient and colour

- Band background: `status-strip` gradient.
- Entry cards: `panel-sheen` over `bg-white/[0.04]`, `border-white/10`.
- Status legend swatches: emerald, amber, and rose at the existing
  `/10` fill and `/30` border opacities.
- Each legend row pairs its swatch with a text label, never colour alone.
- Primary action: `cta-primary`.

### Stellar cue

The section states that the verification result is derived from Stellar
references and revocation state, and it displays a shortened proof/transaction
reference so the on-chain anchor is visible. It also keeps the `Testnet` badge
present, since verification is testnet-only.

---

## Section 8 — Issuer Trust Network

### Title

```text
Who can attest to your income, and how you can check them
```

### Description

Introduces the issuer registry: the organisations that can issue trusted payment
attestations. It previews the public directory with the real fixture rows and
explains what a verifier can inspect about an issuer — registry status,
verification date, disclosed attestation types, and a shortened public wallet
reference. It is careful to state that a registry listing is evidence, not an
endorsement.

### Purpose

Establish that claims do not come from nowhere — they come from identifiable,
inspectable issuers — while staying honest about what registration does and does
not mean.

### Key content

1. **Directory preview table** — the existing `DataPanel` pattern with the real
   rows from `app/issuers/page.tsx`: Veridatum Labs, Stellar Community Fund,
   Anchor Payroll, and Open Work Network, each with verification state, reviewed
   date, and status (`Active` or `Review`).
2. **Metric row** — `18` verified issuers, `16` active issuers, `7` attestation
   types.
3. **Issuer detail preview** — a small card showing what an issuer page contains:
   public wallet reference (`GBC4…8X2K`), registry verification date
   (`2026-07-12`), and disclosed attestation types (Payment, Employment).
4. **Evidence-not-endorsement note** — verbatim intent from
   `app/issuers/veridatum-labs/page.tsx`: registry and Stellar references "are
   evidence, not endorsement", and the page does not claim live contract state.
5. **Trust warning sample** — a short statement that an issuer outside a trusted
   registry surfaces a warning status at verification time, taken from
   `lib/faq-data.ts`.
6. **Directory link** — the primary call to action.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Explore the issuer directory" | `/issuers` | Internal |
| Veridatum Labs detail link | `/issuers/veridatum-labs` | Internal |
| "How issuer trust works" | `/faq` | Internal |

### Gradient and colour

- Background: `stellar-navy` gradient (the brand navy `#0a284a` becomes visible
  here for the first time, tying the section to the logo mark).
- Table: `bg-white/[0.04]` panel with a `bg-slate-300/10` header row, exactly as
  the existing `DataPanel` renders.
- Active status: emerald `#6ee7b7`. Review status: amber `#fcd34d`.
- Attestation chips: `bg-cyan-300/[0.06]`, `border-cyan-300/20`,
  `text-cyan-100`.
- Wallet reference: monospaced, `text-white`.

### Stellar cue

The issuer card shows a shortened Stellar public key and a network reference
line, and the copy explains that issuer trust is recorded in an on-chain
registry — making the "trust" claim concrete and checkable rather than
reputational.

---

## Section 9 — Developers and Integrations

### Title

```text
Build private income verification into your product
```

### Description

The integration pitch for builders: a Verification API, a TypeScript SDK, and
signed webhooks. It shows a short code sample for verifying a proof by ID and
notes the operational guarantees integrators care about — stable schemas,
privacy-safe errors, auditable results, replay protection, and delivery
diagnostics.

### Purpose

Open a second audience — developers — and give them a fast path to the API keys
and documentation they need.

### Key content

1. **Three capability cards** — Verification API ("verify proof IDs or
   credentials with stable schemas, privacy-safe errors, and auditable
   results"), TypeScript SDK ("integrate authentication, verification requests,
   and typed responses with the supported SDK"), and Signed webhooks ("receive
   verification events with replay protection, signature checks, and delivery
   diagnostics"). Taken verbatim from `app/developers/page.tsx`.
2. **Code sample** — a short, monospaced snippet showing a verification call
   against the API base documented in `config/app.ts`
   (`NEXT_PUBLIC_API_URL`, default `http://localhost:4000/api/v1`), with
   server-side-only key handling shown explicitly.
3. **Security note** — a line stating that API keys are server-side secrets and
   are never placed in public environment variables, mirroring the rule in
   `README.md` and `CONTRIBUTING.md`.
4. **Related repositories** — the sibling projects named in `README.md`:
   `earnproof-backend`, `earnproof-contracts`, `earnproof-sdk` (future), and
   `earnproof-specification` (future), with the two future ones clearly marked
   as not yet available.
5. **Developer tools panel** — carrying the existing "Manage API Keys" action
   from `app/developers/page.tsx`.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Developer docs" (primary) | `/developers` | Internal |
| "Manage API keys" | `/developers/api-keys` | Internal |
| "Verification API reference" | `/verify` | Internal |
| Sibling repositories | external, not yet linkable | Only if added to the allowlist |

External link note: GitHub repository links are not in the current allowlist
(`appConfig.helpUrl` and `appConfig.stellarExplorerUrl` only). They must stay
plain text until the allowlist is extended, or be added deliberately as part of
implementation.

### Gradient and colour

- Background: `stellar-navy` gradient, continuing the developer-oriented navy
  band begun in Section 8.
- Capability cards: `panel-sheen`, `border-white/10`.
- Code block: `bg-slate-900` (`#0f172a`) with `border-white/15`, text in
  `text-cyan-200` for keywords and `text-slate-300` for the rest, monospaced.
- Primary button: `cta-primary`.

### Stellar cue

The code sample includes the network passphrase and network identifier from the
environment configuration, so a developer immediately sees that the integration
is network-aware and that the active network must be surfaced in their own UI
too.

---

## Section 10 — Trust, Security, and Testnet Transparency

### Title

```text
Open, non-custodial, and honest about being on testnet
```

### Description

The section that states the project's posture plainly. Four tiles cover the
core commitments — non-custodial, open source, testnet-only today, and a public
security disclosure process — followed by a transparency panel that names the
current limitations outright and links to the system status and accessibility
pages.

### Purpose

Build trust through restraint: state exactly what EarnProof is, is not, and does
not yet do. This is where the "no mainnet promises" rule is honoured on the
landing page.

### Key content

1. **Tile — Non-custodial.** Wallet keys remain with their owners. EarnProof
   cannot move funds or recover seed phrases. (From `app/about/page.tsx`.)
2. **Tile — Open source.** The protocol, schemas, and client libraries are
   inspectable and auditable. (From `app/about/page.tsx`.)
3. **Tile — Testnet only.** EarnProof currently operates on Stellar testnet. No
   mainnet date is announced, and all current proofs are testnet only. Do not
   use mainnet assets or make mainnet promises. (From `lib/faq-data.ts` and
   `README.md`.)
4. **Tile — Security disclosure.** A published process for reporting
   vulnerabilities, linking to `SECURITY.md`, with the note that the current
   supported scope is Stellar testnet only.
5. **Transparency panel** — an explicit "what EarnProof does not do" list:
   no credit decisions, no legal identity verification, no tax certification,
   no loan approval, no seed phrase requests, no storage of raw credentials,
   IP addresses, or wallet activity.
6. **Live status reference** — a small live indicator linking to system status,
   referring to the five tracked services.
7. **Accessibility statement link** — pointing to the accessibility page and its
   published feedback channel.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "System status" | `/status` | Internal |
| "Accessibility" | `/accessibility` | Internal |
| "About EarnProof" | `/about` | Internal |
| "Read the FAQs" | `/faq` | Internal |
| "Security policy" | `SECURITY.md` | Repository file, not a web route |
| "Privacy policy" | `/privacy` | Internal |
| "Terms of use" | `/terms` | Internal |

### Gradient and colour

- Background: `#020617`, flat, so the commitments read as statements rather than
  marketing.
- Commitment tiles: `bg-white/[0.04]` with `border-white/10`.
- Testnet tile: accent treatment — `bg-cyan-300/10`, `border-cyan-300/50`,
  `text-cyan-200` — to mark it as the active network state.
- "Does not do" list markers: rose `#fda4af` bullets, since each line is a
  limitation being acknowledged.
- Section divider: `accent-rule` gradient.

### Stellar cue

The testnet tile is not hidden in small print; it is a first-class commitment
card, and the section explains what the network limitation means in practice for
the user's data.

---

## Section 11 — Pricing Preview

### Title

```text
Free to start on Stellar testnet
```

### Description

A short preview of the pricing model, showing three audience-appropriate tiers —
for workers, for issuers and organisations, and for verifiers and API
integrators — with the testnet plan stated as free. Each tier lists a handful of
representative inclusions, and the highlighted tier uses the accent gradient.
The section is deliberately a preview: the full fee mechanics live on the
pricing page it links to.

### Purpose

Pre-empt the "what does this cost?" question without derailing the narrative,
and hand detailed readers to the dedicated pricing page.

### Key content

1. **Tier 1 — Worker / Individual.** Free on Stellar testnet. Create and share
   proofs, disclosure preview, credential export, and verification links.
   Highlighted as the default entry point.
2. **Tier 2 — Issuer / Organisation.** Issue and manage attestations, issuer
   registry listing, organisation and access settings, and certificate and
   revocation controls as they become available.
3. **Tier 3 — Verifier / API.** Verification API access, API key management,
   signed webhooks, and integration support.
4. **"Free on Stellar testnet" badge** — applied to every tier, since the whole
   product is testnet-only today. This keeps the section honest: nothing is
   billed while the protocol is pre-mainnet.
5. **Comparison row** — a compact strip comparing the three tiers across four
   axes: who it is for, what it unlocks, whether API access is included, and
   whether it is free on testnet.
6. **Fee transparency note** — a line stating that the full fee model and any
   future mainnet pricing will be published on the pricing page rather than
   implied here.
7. **Full pricing link** — the section's single primary call to action.

**Important:** this section must not invent billable prices. Until the pricing
page defines a real model, the tiers are described by capability, and the only
stated price is "free on Stellar testnet", which is already true of the
codebase's testnet-only posture.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "See full pricing" (primary) | `/pricing` | Internal — new page, see Part B |
| "Create a proof" (on the worker tier) | `/proofs` | Internal |
| "Developer docs" (on the verifier tier) | `/developers` | Internal |
| "Issuer directory" (on the issuer tier) | `/issuers` | Internal |

### Gradient and colour

- Background: `#020617`, flat, so the highlighted tier stands out.
- Highlighted tier (Worker/Individual): `cta-primary` gradient border or top
  edge, with `panel-sheen` fill and `border-cyan-300/50`.
- Standard tiers: `bg-white/[0.04]` with `border-white/10`.
- Tier eyebrow labels: `text-cyan-200`, uppercase with tracking.
- "Free on Stellar testnet" badge: `bg-emerald-300/10`,
  `border-emerald-300/30`, `text-emerald-200`.
- Primary button on the highlighted tier: `cta-primary` with `text-slate-950`.

### Stellar cue

Every tier carries the testnet badge rather than a price, which reinforces that
the protocol is in a pre-mainnet phase and that no financial commitment is being
asked for. The badge's emerald colour ties to the app's existing "active" and
"verified" states.

---

## Section 12 — Contact Us

### Title

```text
Talk to the EarnProof team
```

### Description

The closing section: a real contact path with the four enquiry categories the
product already supports — general inquiry, technical support, business
partnership, and security issue — alongside the support address, the
accessibility feedback route, the security disclosure route, and an honest
explanation of exactly what happens when the visitor presses send.

### Purpose

Give every audience a credible next step after the narrative ends, and set
accurate expectations about response and data handling.

### Key content

1. **Enquiry category selector** — General inquiry, Technical support, Business
   partnership, Security issue. Exactly the four categories implemented in
   `components/contact/contact-form.tsx`.
2. **Form fields** — name, email, category, and message, with the same
   validation expectations as the existing form (name 2–100 characters, valid
   email up to 255 characters, message 10–1000 characters) and the same
   accessible error treatment (`role="alert"`, `aria-invalid`,
   `aria-describedby`).
3. **Send action** — the primary button. It must be explained truthfully: the
   existing behaviour is that pressing send opens the visitor's default email
   client with a pre-filled message to `contact@earnproof.com`, and **no message
   content is stored or transmitted by the website**. That transparency sentence
   belongs in this section.
4. **Support address** — `contact@earnproof.com`.
5. **Accessibility contact** — `accessibility@earnproof.com` with the subject
   "Accessibility Feedback", and the published expectation of a response within
   5 business days.
6. **Security contact** — the vulnerability disclosure route, referring to the
   security policy and the current testnet-only supported scope.
7. **Before-you-write FAQ link** — routing common questions to the FAQ so the
   contact channel stays for genuinely new enquiries.
8. **Closing disclaimer** — the EarnProof positioning line and the reminder that
   EarnProof does not provide credit decisions, legal identity verification, tax
   certification, or loan approval. The footer's organisation line — "Veridatum
   Labs builds open infrastructure for verifiable financial data" — is relevant
   context, but the footer itself is out of scope here.

### Links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Send message" (primary) | `mailto:contact@earnproof.com` | External protocol handler |
| "Accessibility feedback" | `mailto:accessibility@earnproof.com?subject=Accessibility%20Feedback` | External protocol handler |
| "Security disclosure" | `SECURITY.md` | Repository file, not a web route |
| "Read the FAQs" | `/faq` | Internal |
| "Contact page" | `/contact` | Internal |
| "Help centre" | `https://help.earnproof.com` | External — already allowlisted |

### Gradient and colour

- Background: `contact-veil` radial gradient, drawing the eye to the form.
- Form panel: `bg-slate-900` (`#0f172a`) or `panel-sheen`, with
  `border-white/15` borders on inputs.
- Input focus: `ring-cyan-300`, matching every existing form in the app.
- Validation errors: `text-red-400` inline, matching the existing contact form.
- Character counter warning: amber `#fcd34d` past 90% of the limit, `red-400`
  past the limit — the exact thresholds already used.
- Primary button: `cta-primary` with `text-slate-950`, plus the existing focus
  ring and offset pattern.
- Informational banner: `bg-cyan-300/10`, `border-cyan-300/50`,
  `text-cyan-200` eyebrow — the existing "How it works" banner treatment.

### Stellar cue

The closing disclaimer keeps the testnet framing present at the moment of
contact, and the security-disclosure route names the testnet-only supported
scope, so a security researcher immediately knows what is in and out of scope.

---

# Part B — Linked Pages (13–15)

These three pages are reached from the landing sections above. Two already exist
in the repository (`/faq` and `/about`) and one is new (`/pricing`). Each entry
records which sections link to it, so the navigation map in the next part can be
checked in both directions.

---

## Page 13 — Pricing

### Route

```text
/pricing
```

Status: **new page, does not exist yet.** It is not in
`scripts/route-manifest.json`, so implementation must add the route, its
metadata (title, description, canonical), and an indexable classification,
consistent with the other public marketing routes.

### Title

```text
Pricing
```

### Description

The full pricing model for EarnProof, told honestly for a protocol that is
pre-mainnet. It explains the three audience tracks — workers, issuers and
organisations, and verifiers and API integrators — states plainly that
everything is free on Stellar testnet today, and describes how protocol and API
metering will work once a real fee model exists. Because no fee schedule is
defined in the codebase, this page describes **what each tier unlocks**, not
invented prices.

### Purpose

Answer the cost question completely for visitors who followed the pricing
preview, without the landing page having to carry commercial detail.

### Linked from

- Section 11 — Pricing Preview (primary call to action).

### Key content

1. **Page heading** — eyebrow "Plans and fees", title "Pricing", description
   summarising that EarnProof is free on testnet and priced by capability.
2. **Testnet-free statement panel** — a prominent emerald-accented panel stating
   that all usage on Stellar testnet is free, that no mainnet date is announced,
   and that no payment is requested at any point in the current product.
3. **Three plan cards** — the same three tiers as Section 11, expanded:
   - **Worker / Individual** — create proofs, disclosure preview, credential
     export, verification links, and on-chain reference lookup.
   - **Issuer / Organisation** — issue and manage attestations, registry
     listing, organisation and access settings, certificate and revocation
     controls as they become available.
   - **Verifier / API** — verification API access, API key management, signed
     webhooks, and integration support.
4. **Comparison table** — a full feature matrix across the three tiers using the
   existing `DataPanel` treatment (headers plus a status badge per row), so it
   matches the issuer directory and status page visually.
5. **What is never charged for** — a short list: verifying a proof, checking
   proof status, reading the issuer directory, reading the documentation, and
   accessibility of the product.
6. **Fee model explanation** — a plain statement that any future fee model will
   be published here before it takes effect, and that mainnet pricing, if it
   ever exists, will be a separately announced change rather than a silent
   update. This follows the release-runbook rule that changing the network is a
   breaking change requiring its own sign-off.
7. **Pricing FAQs** — three or four questions specific to cost:
   "Is it free?", "Will there be a fee later?", "Do I need funds to create a
   proof?", "What happens when mainnet arrives?" Answers drawn from
   `lib/faq-data.ts` where applicable (notably the testnet entries).
8. **Closing call to action** — route the visitor into whichever journey fits.

### Navigation links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Create a proof" (worker tier action) | `/proofs` | Internal |
| "Explore the issuer directory" | `/issuers` | Internal |
| "Developer docs" | `/developers` | Internal |
| "Manage API keys" | `/developers/api-keys` | Internal |
| "Read the FAQs" | `/faq` | Internal |
| "Contact us about a plan" | `/contact` | Internal |
| "Home" (breadcrumb back) | `/` | Internal |
| "Privacy policy" / "Terms of use" | `/privacy`, `/terms` | Internal |

### Gradient and colour

- Page hero band: `hero` gradient.
- Testnet-free panel: `bg-emerald-300/[0.08]`, `border-emerald-300/30`,
  `text-emerald-200` badge.
- Highlighted (Worker) plan card: `cta-primary` top edge or border with
  `panel-sheen` fill.
- Plan cards: `bg-white/[0.04]`, `border-white/10`.
- Comparison table header: `bg-slate-300/10`, matching `DataPanel`.
- Included vs not-included markers in the matrix: emerald `#6ee7b7` for
  included, `text-slate-400` for not included — always with a text label.
- Primary button: `cta-primary` with `text-slate-950`.

### Stellar cue

The page opens with the network state rather than the price: the testnet-free
panel explains that fees are a future question because the protocol is still
pre-mainnet, and that proofs are anchored to Stellar references that any party
can re-check independently.

---

## Page 14 — Frequently Asked Questions

### Route

```text
/faq
```

Status: **already implemented** (`app/faq/page.tsx`, backed by `lib/faq-data.ts`
and listed as an indexable public route in `scripts/route-manifest.json`). This
entry describes the page as the landing page should reference it, not a request
to rebuild it.

### Title

```text
Frequently asked questions
```

### Description

The consolidated answer set for every audience — workers, verifiers, issuers,
and developers. It covers wallet safety, privacy and stored data, verification
behaviour, testnet limits, issuer trust, and proof expiration and revocation.
The page is searchable and its items expand as an accessible accordion.

### Purpose

Catch the long tail of questions so the contact channel and the landing page
stay focused.

### Linked from

- Section 6 — Selective Disclosure and Privacy Controls.
- Section 7 — Verify a Proof (issuer trust explainer).
- Section 8 — Issuer Trust Network ("How issuer trust works").
- Section 10 — Trust, Security, and Testnet Transparency ("Read the FAQs").
- Section 12 — Contact Us ("Read the FAQs").
- Page 13 — Pricing (pricing FAQs cross-reference).
- Page 15 — About EarnProof.

### Key content

The page holds 12 questions across 6 categories, all sourced from
`lib/faq-data.ts`:

1. **Wallet Safety**
   - "Is my wallet safe to use with EarnProof?" — Freighter keeps keys local;
     EarnProof cannot move funds or recover seed phrases; only public keys are
     shared.
   - "Does EarnProof store my wallet keys?" — No. EarnProof is non-custodial;
     keys never leave the device.
2. **Privacy and Data**
   - "What data does EarnProof store about me?" — Only the proof the user
     chooses to share; no raw credentials, IP addresses, or wallet activity.
   - "Can verifiers see my full financial history?" — No; proofs disclose only
     what the issuer attested.
3. **Expiration and Revocation**
   - "Can a proof expire?" — Yes; issuers set expiry dates and an expired proof
     returns EXPIRED status.
   - "What happens if a proof is revoked?" — Verification returns REVOKED and the
     proof can no longer be used.
4. **Testnet**
   - "Is EarnProof on mainnet?" — No; EarnProof currently operates on Stellar
     testnet.
   - "When will mainnet launch?" — No mainnet date is announced.
5. **Verification**
   - "How does proof verification work?" — The verifier checks the proof
     signature, issuer trust, and expiry via Stellar references.
   - "What proof types are supported?" — Only proof types documented in the
     protocol.
6. **Issuer Trust**
   - "How do I know an issuer is trustworthy?" — Check the issuer's DID and trust
     registry listing; EarnProof surfaces an issuer-warning status when an issuer
     is not in a trusted registry.
   - "Can anyone issue proofs?" — Any party can create an issuer DID, but
     verification outcomes reflect issuer trust level.

Supporting elements on the page:

- **Search field** — filters questions and answers, with a clear action that
  restores focus to the search input.
- **Stats row** — total help topics, category count, and the last reviewed date.
- **Accordion items** — each with `aria-expanded` and `aria-controls`, a rotated
  chevron, and an answer region labelled by its question. Open answers are not
  height-clamped, so long translations and 40% text expansion are never cut off.
- **Empty state** — a no-results message when the search matches nothing.

### Navigation links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Contact us" (unanswered question) | `/contact` | Internal |
| "Privacy policy" | `/privacy` | Internal |
| "Verify a proof" | `/verify` | Internal |
| "System status" | `/status` | Internal |
| "Proof types" | `/proof-types` | Internal |
| "About EarnProof" | `/about` | Internal |

### Gradient and colour

- Page background: `#020617`, flat, matching the existing page.
- Accordion items: `bg-white/[0.04]`, `border-white/10`, with a
  `hover:bg-white/[0.06]` and `focus-visible:ring-2 ring-cyan-300` interaction.
- Category badge: `bg-cyan-300/10`, `border-cyan-300/50`, `text-cyan-200`.
- Chevron icon: `text-cyan-200`.
- Stats cards: `bg-white/[0.04]`, `border-white/10`.
- No gradients are required here; consistency with the existing page matters
  more than novelty.

### Stellar cue

The testnet and verification categories keep the network present throughout:
answers state that verification resolves through Stellar references and that all
proofs are testnet-only today.

---

## Page 15 — About EarnProof

### Route

```text
/about
```

Status: **already implemented** (`app/about/page.tsx`, listed as an indexable
public route in `scripts/route-manifest.json`). This entry describes the page as
the landing page should reference it, and the additional blocks it would need to
carry the full "company" role.

### Title

```text
About EarnProof
```

### Description

The page that explains who stands behind the protocol and what the project is
committed to. It covers the steward organisation, the open-source and
non-custodial commitments, the choice to build on Stellar, the privacy-first
design principles, and — stated plainly — the roadmap position that mainnet is
not yet announced. It is the landing page's credibility anchor.

### Purpose

Answer "who is behind this, and do they behave responsibly?" without the landing
page having to carry organisational and governance content.

### Linked from

- Section 2 — Live on Stellar (network and infrastructure context).
- Section 10 — Trust, Security, and Testnet Transparency ("About EarnProof").
- Page 14 — Frequently asked questions.

### Key content

1. **Page heading** — the existing heading and description: "About EarnProof" /
   "Open infrastructure for portable, privacy-preserving financial evidence."
2. **Hero card** — the existing card with the "Open protocol" status badge, the
   title, the description, and the "Explore the protocol" action linking to
   `/how-it-works`.
3. **Three commitment cards** — the existing cards, kept verbatim:
   - **Open source** — the protocol, schemas, and client libraries are
     inspectable; ownership and implementation are transparent and auditable
     policy.
   - **Non-custodial** — wallet keys remain with their owners; EarnProof cannot
     move funds or recover seed phrases.
   - **Built on Stellar** — Stellar references and Soroban commitments produce
     portable, independently verifiable evidence.
4. **Steward organisation block** — the organisation name "Veridatum Labs" and
   its positioning line: "Veridatum Labs builds open infrastructure for
   verifiable financial data." The organisation is already referenced on the
   privacy page and in the footer.
5. **Design principles block** — the privacy and UX requirements from
   `README.md` restated as product principles: show testnet status on relevant
   screens, hide sensitive amounts by default, show a disclosure preview before
   proof creation, distinguish every verification state, never expose full wallet
   history, and never place signing material in client code.
6. **Protocol components block** — the four cooperating projects named in
   `README.md`: `earnproof-backend` (API, payment indexing, proof generation,
   credential signing, verification), `earnproof-contracts` (Soroban issuer
   registry, proof commitment registry, revocation state, protocol
   configuration), `earnproof-sdk` (future TypeScript SDK), and
   `earnproof-specification` (future credential and verification standard). The
   two future projects must be labelled as not yet available.
7. **Roadmap block** — an honest status ladder rather than dates:
   - Shipped: wallet challenge signing, payment sync and classification,
     minimum-income proof creation, public verification, issuer directory shell,
     status page, and this documentation set.
   - In progress: proof revocation controls, a richer worker dashboard, and
     verification-state component tests.
   - Not announced: mainnet. The block must state that there is no mainnet date.
8. **Contribution block** — a link to the contribution guidance and code of
   conduct for people who want to help.
9. **Closing call to action** — route to the product or the docs.

### Navigation links and buttons

| Element | Destination | Kind |
| --- | --- | --- |
| "Explore the protocol" | `/how-it-works` | Internal |
| "Proof types" | `/proof-types` | Internal |
| "Developer docs" | `/developers` | Internal |
| "System status" | `/status` | Internal |
| "Privacy policy" | `/privacy` | Internal |
| "Terms of use" | `/terms` | Internal |
| "Accessibility" | `/accessibility` | Internal |
| "Contact us" | `/contact` | Internal |
| "Read the FAQs" | `/faq` | Internal |
| "Contributing" | `CONTRIBUTING.md` | Repository file, not a web route |
| "Code of conduct" | `CODE_OF_CONDUCT.md` | Repository file, not a web route |
| "Security policy" | `SECURITY.md` | Repository file, not a web route |
| Related repositories | external, not yet allowlisted | Plain text until allowlisted |

### Gradient and colour

- Page hero band: `hero` gradient.
- Hero card: `panel-sheen` over `bg-white/[0.04]`, `border-white/10`.
- "Open protocol" badge: `bg-cyan-300/10`, `border-cyan-300/50`,
  `text-cyan-200` with uppercase tracking — the existing `StatusBadge`.
- Commitment cards: `bg-white/[0.04]`, `border-white/10`.
- Roadmap ladder: emerald for shipped, amber for in progress, and
  `text-slate-400` for "not announced" — each with a text label, never colour
  alone.
- Primary button: `cta-primary` with `text-slate-950`.

### Stellar cue

The "Built on Stellar" card is one of the three headline commitments, and the
protocol components block names the Soroban contracts project directly, so the
organisational story is inseparable from the blockchain architecture.

---

# Navigation Map

This map shows every destination the landing page and its linked pages expose,
so the graph can be read in both directions.

## Section to destination

| From | Destination | Kind | Note |
| --- | --- | --- | --- |
| Section 1 — Hero | `/proofs` | Internal | Primary call to action |
| Section 1 — Hero | `/verify` | Internal | Secondary call to action |
| Section 1 — Hero | `/how-it-works` | Internal | Tertiary text link |
| Section 2 — Live on Stellar | `/status` | Internal | Live system status |
| Section 2 — Live on Stellar | `https://horizon-testnet.stellar.org` | External | Needs allowlist entry, otherwise plain text |
| Section 3 — The Problem | `/privacy` | Internal | Privacy policy |
| Section 3 — The Problem | `/proof-types` | Internal | Selective disclosure detail |
| Section 4 — How It Works | `/how-it-works` | Internal | Full walkthrough |
| Section 4 — How It Works | `/proofs` | Internal | Start a proof |
| Section 5 — Proof Types | `/proof-types` | Internal | Full catalogue |
| Section 5 — Proof Types | `/proofs` | Internal | Create a proof |
| Section 5 — Proof Types | `/proof-types/minimum-income` | Internal | Available type detail |
| Section 6 — Selective Disclosure | `/privacy` | Internal | Privacy policy |
| Section 6 — Selective Disclosure | `/proof-types` | Internal | Proof types |
| Section 6 — Selective Disclosure | `/faq` | Internal | Page 14 |
| Section 7 — Verify a Proof | `/verify` | Internal | Primary verification portal |
| Section 7 — Verify a Proof | `/verify/credential` | Internal | Credential upload |
| Section 7 — Verify a Proof | `/verify/scan` | Internal | QR scan |
| Section 7 — Verify a Proof | `/issuers` | Internal | Issuer trust explainer |
| Section 8 — Issuer Trust Network | `/issuers` | Internal | Directory |
| Section 8 — Issuer Trust Network | `/issuers/veridatum-labs` | Internal | Issuer detail |
| Section 8 — Issuer Trust Network | `/faq` | Internal | Issuer trust answers, Page 14 |
| Section 9 — Developers | `/developers` | Internal | Developer docs |
| Section 9 — Developers | `/developers/api-keys` | Internal | API key management |
| Section 9 — Developers | `/verify` | Internal | Verification reference |
| Section 10 — Trust and Transparency | `/status` | Internal | System status |
| Section 10 — Trust and Transparency | `/accessibility` | Internal | Accessibility statement |
| Section 10 — Trust and Transparency | `/about` | Internal | Page 15 |
| Section 10 — Trust and Transparency | `/faq` | Internal | Page 14 |
| Section 10 — Trust and Transparency | `/privacy`, `/terms` | Internal | Legal pages |
| Section 10 — Trust and Transparency | `SECURITY.md` | Repository file | Not a web route |
| Section 11 — Pricing Preview | `/pricing` | Internal | Page 13 — new route |
| Section 11 — Pricing Preview | `/proofs`, `/developers`, `/issuers` | Internal | Tier-specific actions |
| Section 12 — Contact Us | `mailto:contact@earnproof.com` | Protocol handler | Existing form behaviour |
| Section 12 — Contact Us | `mailto:accessibility@earnproof.com` | Protocol handler | Subject: Accessibility Feedback |
| Section 12 — Contact Us | `/contact` | Internal | Full contact page |
| Section 12 — Contact Us | `/faq` | Internal | Page 14 |
| Section 12 — Contact Us | `https://help.earnproof.com` | External | Already allowlisted |
| Section 12 — Contact Us | `SECURITY.md` | Repository file | Not a web route |

## Page to destination

| From | Destination | Kind |
| --- | --- | --- |
| Page 13 — Pricing (`/pricing`) | `/proofs`, `/issuers`, `/developers`, `/developers/api-keys`, `/faq`, `/contact`, `/`, `/privacy`, `/terms` | Internal |
| Page 14 — FAQ (`/faq`) | `/contact`, `/privacy`, `/verify`, `/status`, `/proof-types`, `/about` | Internal |
| Page 15 — About (`/about`) | `/how-it-works`, `/proof-types`, `/developers`, `/status`, `/privacy`, `/terms`, `/accessibility`, `/contact`, `/faq` | Internal |
| Page 15 — About (`/about`) | `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md` | Repository files |

## Inbound map for the three linked pages

| Page | Inbound from |
| --- | --- |
| `/pricing` (Page 13) | Section 11 |
| `/faq` (Page 14) | Sections 6, 7, 8, 10, 12; Pages 13 and 15 |
| `/about` (Page 15) | Sections 2 and 10; Page 14 |

---

# Summary of the 15 items

| # | Item | Type | Route |
| --- | --- | --- | --- |
| 1 | Hero | Landing section | `/` |
| 2 | Live on Stellar | Landing section | `/` |
| 3 | The Problem | Landing section | `/` |
| 4 | How It Works | Landing section | `/` |
| 5 | Proof Types and Capabilities | Landing section | `/` |
| 6 | Selective Disclosure and Privacy Controls | Landing section | `/` |
| 7 | Verify a Proof | Landing section | `/` |
| 8 | Issuer Trust Network | Landing section | `/` |
| 9 | Developers and Integrations | Landing section | `/` |
| 10 | Trust, Security, and Testnet Transparency | Landing section | `/` |
| 11 | Pricing Preview | Landing section | `/` |
| 12 | Contact Us | Landing section | `/` |
| 13 | Pricing | Linked page | `/pricing` (new) |
| 14 | Frequently Asked Questions | Linked page | `/faq` (existing) |
| 15 | About EarnProof | Linked page | `/about` (existing) |

---

# Out of scope

- The header navbar and the footer, and their navigation labels. Both are
  existing shared shell components and are excluded from the 15 items.
- Any landing page code, component, or style implementation. This document is a
  specification for review.
- Invented pricing. Page 13 describes capability tiers and the testnet-free
  state; it does not state billable amounts, because no fee model exists in the
  codebase.
- External links that are not in the current allowlist. Anchors to Horizon,
  stellar.expert, or GitHub must either go through
  `components/common/external-link.tsx` after an allowlist update, or remain
  plain text.
- Header-level search, language switching, and account menus, which belong to
  the excluded header rather than to a landing section.

---

# Notes for implementation (later, not part of this deliverable)

1. A landing page section count above 12, or a new linked page, should be
   reflected in this document first, so it stays the single source of truth for
   landing page structure.
2. `/pricing` needs a route manifest entry, metadata, and a canonical URL before
   implementation, following the pattern in
   `scripts/generate-route-manifest.js`.
3. Every internal link above should be checked with `npm run validate:links`
   after implementation.
4. Verification-state colours must stay identical to the app's existing
   emerald, amber, and rose treatment, so a proof looks the same wherever it is
   displayed.
5. The testnet badge must remain visible on every section that references
   network state.
6. Body text on any gradient section must keep a readable contrast ratio, and
   gradients must never be the sole carrier of meaning.
