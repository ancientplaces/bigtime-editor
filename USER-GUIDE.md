**Status:** Active
**Last updated:** 2026-06-24
**Supersedes:** —
**Superseded by:** —

# Big Time MIDI Editor — Quick Guide

A web-based editor for controlling the Chase Bliss **Big Time** delay over MIDI, right from your browser.

**Live:** https://ancientplaces.github.io/bigtime-editor/

> ⚠️ **Very new, largely untested.** This is an early release. The control map is verified against Chase Bliss's locked-in MIDI spec, but the editor itself hasn't been road-tested against the hardware much yet. Expect rough edges, double-check anything important, and please report anything that seems off.

---

## What you need

- **A Chromium browser** — Chrome or Edge (desktop, or Chrome on Android). The editor uses the **Web MIDI API**, which **Firefox and iOS Safari do not support.**
- **A MIDI interface** connecting your computer to the Big Time's 5-pin MIDI IN.
- The pedal set to the right **MIDI channel** (Big Time defaults to channel **2**).

## How the browser MIDI works

1. Open the site. Your browser will ask for permission to **control MIDI devices** — choose **Allow**. (Chrome remembers this per-site, so you'll usually only see it once.)
2. The dot by the title turns green and reads **"MIDI ready."** Important: that only means the *browser* granted access — it does **not** mean a device is connected yet.
3. Pick your interface from the **Select MIDI Output** dropdown, and set **CH** to match your pedal.
4. Now move a fader or tap a button — it sends that change to the pedal in real time. If nothing's selected in the dropdown, controls do nothing and you'll get a "Select a MIDI output first" nudge.

**It's a one-way street.** The Big Time doesn't send its settings *back* out over MIDI. So the editor can't read the pedal's current state — if you change something on the hardware, or load a preset on the pedal, the editor won't know. After doing either, click **▶ Send All Parameters** to push the editor's values back onto the pedal so the two are in sync.

## Dark & light mode

Use the **☀ / ☾ toggle** in the top-right of the header to switch between the dark theme and a cream "Lexicon"-style **light mode**. Your choice is remembered in that browser for next time.

## Presets — read this carefully

There are **two different "save" systems**, and they are not the same thing:

### 1. Pedal slots (saved on the hardware — durable, but no names)
- **Save to Slot** / **Save to Current Slot** write the *current settings* into the Big Time's own memory (slots 0–126). These live on the pedal permanently.
- **Recall** loads a slot back.
- ⚠️ The pedal stores presets **by number only — it has no names.** The "Preset name…" field is **not** sent to the pedal.

### 2. Local named presets (saved in your browser — named, but fragile)
- **+ Save Local State** snapshots everything in the editor *with the name you type* and stores it in your browser.
- These survive reloads and revisits — **but only in that one browser on that one device.** They're lost if you clear browsing data, switch browsers/computers, or use private/incognito mode.

### The dependable way to truly keep your presets
Use **Export.** It downloads a `bigtime-presets.json` file with every named preset and its full settings. Keep that file somewhere safe (Drive, Dropbox, etc.). **Import** loads it back on any browser or machine.

> **Recommended habit:** after building presets you care about, hit **Export** and back up the file. That JSON is the only portable, durable record of your preset *names*; the pedal durably holds the *settings* (by number) on its own.

## The tabs, briefly

- **Controls** — main faders/buttons and the SHIFT-layer "alt" faders/buttons.
- **Performance** — loop-mode footswitch commands, play/dub behavior, and tap-tempo subdivision.
- **System & MIDI** — options menu, MIDI clock mode, global-notes mode, and EOM (expression over MIDI).
- **Exp / CV** — *reference/planning only.* Expression/CV assignment is set physically on the pedal; there's no MIDI command to configure it remotely. Use this tab to note your intended assignments. For real-time expression over MIDI, use **EOM** on the System & MIDI tab.

## Keyboard & accessibility

Faders and buttons are keyboard-operable: **Tab** to a control, **Enter/Space** to toggle a button, and **arrow keys** (plus PageUp/PageDown, Home/End) to move a focused fader.

## Known limitations

- No Web MIDI in Firefox or on iOS Safari.
- The editor can't read the pedal's state (one-way MIDI) — use **Send All Parameters** to re-sync.
- Local preset *names* are browser-bound; use **Export** to back them up.
- Early software — verify critical settings against the pedal.

## Feedback

Found a bug or something confusing? Please pass it along — that's exactly what this early release is for.
