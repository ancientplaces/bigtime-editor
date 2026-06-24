# Big Time — MIDI Editor

A web-based MIDI editor for the Chase Bliss **Big Time** delay.

Single self-contained `index.html` (no build step, no dependencies beyond a Google Fonts link). Open it locally in a browser, or use the hosted version below.

## Live

https://ancientplaces.github.io/bigtime-editor/

## Local use

Open `index.html` in any modern browser. For MIDI access (Web MIDI API), use Chrome or Edge over `http://localhost` or `https://`. On first use the browser will ask permission to control MIDI devices — choose Allow. The green "MIDI ready" dot means the browser granted access; you still need to pick a device from the **Select MIDI Output** dropdown before anything is sent.

## MIDI spec reference

The CC map in this editor is verified against the locked-in Big Time MIDI specification: **`Big-Time-MIDI-manual-locked-2026.pdf`** (ref 2026 – BT001, released via the Chase Bliss Discord).

> ⚠️ The PDF currently hosted on chasebliss.com/big-time is an earlier, error-ridden revision (binary THRU/OUT clock, a phantom CC 111, a value-12 whole note, and different alt-button CCs). Use the bundled PDF as the source of truth, not the website version.

## Notes / known limitations

- **Exp/CV tab is reference/planning only.** Big Time's expression/CV assignment and heel–toe range are set physically on the pedal; there is no MIDI command to configure them remotely. For real-time expression over MIDI, use **EOM** (CC 100) on the System & MIDI tab.
- Web MIDI is not supported in Firefox or on iOS Safari.
