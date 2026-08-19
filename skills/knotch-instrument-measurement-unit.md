---
name: Instrument a page with the Knotch Measurement Unit
description: >-
  Embed the Knotch tag on a publisher page, control Measurement Units at runtime with the
  browser-side Knotch Unit API, and honour visitor opt-out.
api: components/knotch-components.yml
operations:
  - Knotch.addUnit
  - Knotch.removeUnit
  - Knotch.setFocus
  - Knotch.enableUnit
  - Knotch.disableUnit
  - Knotch.setOptout
generated: '2026-08-13'
method: generated
source: >-
  Grounded in https://docs.knotch.it/unit/, https://docs.knotch.it/unit_api/ and
  https://docs.knotch.it/unit_optout/
---

# Instrument a page with the Knotch Measurement Unit

This is a **browser-side** surface. There is no REST API and no SDK for it — the contract is a
global `Knotch` object installed by a script tag. Everything here is documented by Knotch at
docs.knotch.it.

## Step 1 — Decide the Unit type

- **Feedback Unit** renders a sentiment question. Captures Time to Interact and Sentiment Based
  Response, plus everything the Invisible Unit captures.
- **Invisible Unit** renders nothing. Still captures page and unique views, time on page, time
  playing video, referrer source, device and browser, scroll depth, geolocation and third-party
  demographics.

## Step 2 — Choose the integration

- **JavaScript tag** — script in the page, placeholder `<div>` where the Unit should appear.
  Rendered in the page context, so Knotch gets the **full** measurement set.
- **iframe** — nested browsing context, more isolated, but Knotch explicitly cannot measure scroll
  depth, referrers or viewability.
- **Video** — add the `data-Knotch` attribute to an existing `<video>` element. The Unit appears
  when playback ends, and will not re-appear on replay once a visitor has responded.

Pick the JavaScript tag unless isolation is a hard requirement; the iframe silently costs you
metrics.

## Step 3 — Embed

```html
<body>
  <div name="Unit 1" class="knotch_1"></div>
  <script src="https://www.knotch-cdn.com/unit/latest/knotch.js"></script>
</body>
```

The placeholder's Unit ID is carried in the class name: `knotch_<unitId>`.

Note the `latest` path segment. Knotch documents no versioned URL and publishes no SRI hash, so
you cannot pin the build you ship. Flag that to whoever owns your CSP and change control.

## Step 4 — Hold a Unit back, then enable it

Add `knotch-ignore` to any placeholder that should **not** inject on page load:

```html
<div knotch-ignore="true" name="disabled unit" class="knotch_1"></div>
```

Then use the runtime API:

- `Knotch.addUnit(id)` — removes `knotch-ignore` and injects the Unit.
- `Knotch.removeUnit(id)` — un-injects it and puts `knotch-ignore` back.
- `Knotch.setFocus(id)` — injects that Unit and removes **every other** Unit on the page. Use this
  for single-Unit-at-a-time layouts such as tabs or carousels.
- `Knotch.enableUnit(id)` — re-displays a hidden Unit and **resumes tracking where it left off**.
- `Knotch.disableUnit(id)` — hides the Unit and pauses collection.

`enableUnit`/`disableUnit` are the pause-and-resume pair; `addUnit`/`removeUnit` are the
inject-and-tear-down pair. They are not interchangeable — `removeUnit` discards the Unit, while
`disableUnit` preserves its in-progress state.

Every method takes the Unit ID and it is documented as required.

## Step 5 — Honour opt-out

Knotch sets a unique-visitor cookie on `.knotch.it`. Defaults: visitors are opted **in**, except
in EU countries, where opt-out defaults to **true**.

- With the tag on the page: `Knotch.setOptout(true)` to opt out, `Knotch.setOptout(false)` to opt in.
- Without the tag on that page: set `knotch_optout=0` on your own domain. `0` means *requested but
  not yet applied*. The next time the visitor hits a page carrying the Knotch script, Knotch reads
  the cookie, calls `setOptout(true)`, and rewrites it to `knotch_optout=1` to mark it done.
- To opt everyone out by default, set `knotch_optout=0` site-wide.

Be precise about the effect when reporting to stakeholders: opting out changes **only the unique
visitors count**, which converges toward page views. Time on page, scroll depth, responses and
referral sources keep being collected.

## Related

- Fire arbitrary conversion or journey events from the page with the Event Pixel:
  `https://t.knotch.it/receive/beacon.gif?account_id=<id>&event=<name>&page_url=<url>&ts=<ms>`
  (see `components/knotch-components.yml`).
- Send server-side outcomes instead: `skills/knotch-send-conversion-events.md`.
