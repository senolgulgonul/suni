# Sun’î

An artificial composer that improvises Turkish makam **taksim** in the browser, voiced with a sampled, microtonal (fretless) acoustic guitar. Single HTML file, no dependencies, fully offline.

**Live demo:** https://senolgulgonul.github.io/suni/

> The name is a mahlas (a classical composer's pen name) in the old style of Itrî or Zekâî. It reads like one, and it also means "artificial": a composer that works the makam by calculation. The project started life as *Neyron* (from *ney*), then traded the flute for a guitar.

---

## What it is

Press **Play** and Sun’î starts composing a taksim, phrase after phrase, and keeps going until you press **Stop**. The melody is generated live in your browser from the rules of the chosen makam, then played through real recorded guitar notes that are pitch-shifted to the exact comma frequencies, so the guitar plays true microtones it could never fret.

Nothing is pre-baked: every run is a different improvisation, but always recognizably in the same makam.

## Features

- **Endless live taksim**, generated phrase by phrase until you stop it.
- **14 makams**: the 13 basic (*basit*) makams of Turkish music plus Segâh.
- **True microtones** from the AEU 53-comma system (not 12-tone equal temperament).
- **A fretless guitar voice**: real acoustic-guitar samples, pitch-shifted per note to the exact makam comma.
- **Perde ribbon** that lights the sounding pitch in real time, with the güçlü and karar marked.
- **Save / Open** a piece as a small JSON file (the exact note sequence), and **Export WAV** (mono) of the current taksim.
- **Tempo** control and a **makam** selector.
- One file, no build step, no network calls, no tracking.

## The makams

Çârgâh, Bûselik, Kürdî, Rast, Uşşâk, Nevâ, Hümâyun, Hicaz, Uzzâl, Zirgüleli Hicaz, Hüseynî, Karcığar, Basit Sûzinâk, and Segâh.

A nice pair to compare: **Hicaz** and **Uzzâl** share the same scale but pull toward a different dominant, so they sound related yet distinct.

## How it works

**The composer (generation).** A seyir-aware weighted random walk over the makam's perdes. The starting region is set by the makam's seyir (ascending, descending, or descending-ascending). Motion is mostly stepwise with a directional bias, plus a gravitational pull toward the güçlü (dominant) in the middle of a phrase and toward the karar (final) at phrase ends. Phrase endings lock onto *asma karar* (secondary-cadence) perdes, and the closing phrase resolves with the `yeden -> durak` (leading-tone to tonic) formula. So the result is random but never arbitrary: it stays inside the grammar of the makam.

**The pitches (microtones).** Frequencies come from the Arel-Ezgi-Uzdilek 53-comma system. Each perde is an exact number of commas above the durak, converted to Hz with `durak * 2^(comma/53)`. No rounding to piano keys.

**The voice (sampled fretless guitar).** A handful of real acoustic-guitar notes are embedded in the page. For every note, Sun’î picks the nearest sample and resamples it (via `playbackRate`) to the exact target frequency. Because the shift is continuous, the guitar lands precisely on each comma, which a fretted guitar physically cannot do. A light body shelf, a gentle bus compressor, and a small convolution reverb finish the tone.

## Usage

| Control | What it does |
| --- | --- |
| **Play / Stop** | Start the endless taksim, or stop it. |
| **New** | Compose a fresh taksim in the current makam (without starting playback). |
| **Makam** | Choose the makam. Changing it loads a new improvisation. |
| **Tempo** | Speed of the playback. |
| **Save** | Download the current piece as a small JSON file (exact notes). |
| **Open** | Load a saved piece and replay it exactly. |
| **WAV** | Render the current taksim to a mono WAV file. |

Audio starts only after you press Play, as browsers require.

## Run it

It is one self-contained HTML file.

- **Locally:** open the file in any modern browser. That is all.
- **GitHub Pages:** rename the file to `index.html`, push it, and enable Pages for the repo. You can keep the timestamped version alongside as an archive.

No server, no bundler, no dependencies.

## Credits and license

- **Guitar samples:** [tonejs-instruments](https://github.com/nbrosowsky/tonejs-instruments), licensed **CC-BY 3.0**. The samples are embedded and pitch-shifted; attribution is also shown in the app footer.
- **Code:** MIT (see `LICENSE`). Adjust to taste.

If you redistribute, keep the CC-BY attribution for the guitar samples.

## Notes

- Everything (including the guitar samples, base64-encoded) lives in the single HTML file, so there are no external requests and it works offline.
- Makam theory is a deep field, and these are practical, playable models rather than exhaustive treatments. Corrections and additional makams are welcome.
