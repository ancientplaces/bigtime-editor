**Status:** Active
**Last updated:** 2026-06-24
**Supersedes:** —
**Superseded by:** —

# Big Time MIDI Editor — Revision Spec (for Antigravity)

Apply these changes to `index.html`. **Do not alter the visual design** — keep the existing fonts (Jost / Share Tech Mono), the CSS variables, the faceplate/wood styling, and all control appearances. Every change below is either non-visual logic, an invisible tag, or styling that reuses the existing palette and only activates on small screens / keyboard focus.

## Context

The CC map was verified against the locked-in MIDI spec (`Big-Time-MIDI-manual-locked-2026.pdf`, ref 2026 – BT001). **The CC map is correct — do not change any CC numbers or value ranges.** These revisions are robustness, accessibility, and honesty fixes only.

## 1. Guard localStorage (prevents a blank-page crash)

A corrupt or blocked `localStorage` currently throws at startup and the whole app fails to render.

- **Read:** wrap the initial `appPresets` load in `try/catch`, defaulting to `[]`, and force `[]` if the parsed value isn't an array.
- **Write:** wrap `localStorage.setItem` in `savePresetStorage()` in `try/catch`; on failure show an error toast ("Could not save presets — browser storage is blocked").

## 2. Feedback when no MIDI output is selected

`sendCC` / `sendPC` silently do nothing when no output is selected, which confuses testers who don't have the pedal.

- Add a throttled `warnNoOutput()` helper (fires an error toast "Select a MIDI output first" at most once per ~2.5 s so dragging a fader doesn't spam).
- Call it from the `else` branch of both `sendCC` and `sendPC`.

## 3. Wire the "Save to Current Slot" button (CC 28)

The function `saveToCurrent()` (sends CC 28) already exists but has no button.

- Add a `btn`-styled button in the Presets card, between "Save to Slot" and "+ Save Local State", labelled **Save to Current Slot**, `onclick="saveToCurrent()"`, with a tooltip noting it's CC 28.

## 4. Exp/CV tab — make it honest (reference only)

There is no MIDI command to assign Exp/CV or set a heel–toe range; that's done physically on the pedal. The tab currently implies otherwise and the assignment toggle sends a bogus "fader to max" CC.

- **Remove** the `sendCC(f.cc, 127)` call from the Exp toggle handler. The toggle should only set its visual state and show a "planning note" toast (no MIDI sent).
- **Reword** the info box: keep the "How it works on the pedal" paragraph; replace the second paragraph to state this tab is reference/planning only, that assignment + heel/toe are set on the hardware, and that real-time expression over MIDI uses EOM (CC 100) on the System & MIDI tab.

## 5. Favicon + share tags (invisible)

- Add `<meta name="description">`, `og:title`, `og:description`, `og:type`, and `theme-color` (#18191c) in `<head>`.
- Add an inline SVG data-URI favicon: dark rounded square (#18191c) with a cyan ring (#3dd6c8) and a small pink center dot (#f06090) — matches the brand palette.

## 6. Mobile responsive (desktop layout unchanged)

- Add `class="tab-cols"` to the three two-column wrapper `<div>`s in the Controls, System & MIDI, and Performance tabs (the ones with `style="display: flex; gap: 32px;"`).
- Add a single `@media (max-width: 880px)` block that: reduces body padding, lets the chassis grow vertically, stacks `#body` (sidebar drops below main), and switches `.tab-cols` to a single column (removing the inner right-border/padding). No effect above 880px.

## 7. Keyboard accessibility (no visual change)

The faders, segment buttons, toggles, exp-toggles, and tabs are `<div>`s — not keyboard reachable. (The loop, subdivision, tap, and preset buttons are already real `<button>`s.)

- Add a `:focus-visible` outline (2px solid `--cyan`, 2px offset) for those div controls.
- Add `a11yEnhance()` that gives each `.fader-track / .seg-btn / .toggle / .exp-toggle / .tab` a `tabindex` and appropriate `role` (slider / tab / button), plus `aria-valuemin/max/now` on faders. Call it once at init and re-run via a `MutationObserver` on `#main` so it survives rebuilds.
- Add a delegated `keydown` listener: Enter/Space activates the button-like divs; Arrow/PageUp/PageDown/Home/End adjust a focused fader. Update `aria-valuenow` in `setFader`.

## Verification

- `node --check` the script: no syntax errors.
- CC map unchanged from the locked spec.
- Page renders identically on desktop; controls now keyboard-operable; narrow window stacks cleanly.
