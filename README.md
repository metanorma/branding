# Metanorma branding

Brand assets for Metanorma (logos in `logo/`, see `CLAUDE.md` for the naming
convention and asset rules) plus `lighthouse.js` — the animated Metanorma
lighthouse icon as a dependency-free ES5 component.

## Lighthouse — animated icon

A self-contained, zero-dependency SVG animation of the Metanorma lighthouse:
a 3D-projected rotating beacon with a cinematic pass (Searchlight-Pictures
style), scrolling sea, day/night scenes, and playful interactions.

Open `index.html` to see the demo (dark "evening" and light "morning" scenes
side by side).

### Quick start

```html
<div id="icon"></div>
<script src="lighthouse.js"></script>
<script>
    var lh = new Lighthouse('#icon', { theme: 'dark', beamPeriod: 6.5 });
</script>
```

No build step, no dependencies. The container is filled with a responsive
`<svg viewBox="0 0 147.4 147.4">`; size it with CSS.

### Interactions

- **Move the pointer** — aim the beam (X sweeps, Y pitches up/down)
- **Quick click** — flash + spin "kick" to the beacon
- **Long-press** — the lamp signals Morse SOS (`... --- ...`)
- **Konami code** (`↑↑↓↓←→←→BA`) — party mode
- **Day/night** — in the light ("morning") theme the lamp rests until an
  interaction wakes it; at night it is always on duty

Ambient surprises: a shooting star by night, gulls by day (`ambient: false`
to disable).

### Options

All options are optional; units are the 147.4 × 147.4 icon space.
Full documentation is in the JSDoc block above the constructor in
`lighthouse.js`. Summary:

| Group | Options (default) |
| --- | --- |
| Scene | `theme` `'dark'\|'light'\|object` (`'dark'`) · `mode` `'rotate'\|'static'` · `delay` ms |
| Rotation | `beamPeriod` s (7.5, alias `period`) · `beamCount` (2) · `beamElev` (0.26) · `beamNodAmp`/`beamNodPeriod` (0.07 / 5.3) |
| Beam shape | `beamLen` (190) · `beamApexHw`/`beamTipHw` (2.3 / 7.0) · `beamWidBoost` (1.2) · `beamMinBright`/`beamMaxBright` (0.3 / 1.0) · `beamHazeScale`/`beamHazeOpacity` (2.2 / 0.5) |
| The pass | `passSigma` (0.16) · `bloomRadius`/`bloomPeak` (78 / 0.95) · `flareRx`/`flareRy`/`flarePeak` (88 / 2.6 / 0.85) · `washRadius`/`washPeak` (180 / 0.2) · `coreRadius` (3.4) |
| Lamp | `pilotRadius`/`pilotOpacity` (8 / 0.6) · `restLevel` (theme: 1 dark, 0.05 light) |
| Icon response | `rayGlow` (0.9) · `waveGlintPeak`/`waveGlintTravel` (0.45 / 100) |
| Wave | `waveSpeed` (16) · `waveFeather` (0.12) |
| Interaction | `aimSensitivity`/`aimElevSpan` (55 / 55) · `clickBoost`/`boostDecay` (2.4 / 1.9) · `holdDelay` (550) · `morsePattern`/`morseUnit` (`'... --- ...'` / 95) |
| Click flash | `haloRadius`/`haloPeak` (60 / theme) · `shockColor`/`shockMax`/`flashDuration` (theme / 130 / 0.85) |
| Fun | `ambient` (true) · `partyDuration`/`partySpin` (8000 / 2.6) |

Derivation rules: `period` aliases `beamPeriod`; `haloPeak` and `restLevel`
default from the theme; `bloomPeak`/`flarePeak`/`washPeak` scale with
`haloPeak`. An option set explicitly always wins.

### Themes and custom palettes

Two named scenes: `'dark'` (evening: lamp always on duty, deep indigo sea,
shooting stars) and `'light'` (morning: resting lamp, sunlit teal sea, gulls).

Or pass a palette object — any key you skip falls back to `base`:

```js
new Lighthouse('#icon', {
    theme: {
        base: 'dark',                    // 'dark' | 'light'
        beam: '#eaf7ff',                 // beam, beamGlow, beamTail, halo, shock
        bodyFrom: '#e8f0ff',             // tower: body | bodyFrom+bodyTo | bodyStops+bodyGrad
        bodyTo: '#5a7cc8',
        waveFrom: '#6fa8dc',             // sea:   wave | waveFrom+waveTo | waveStops
        waveTo: '#0b2a5b',
        day: false,                      // morning behaviors; default: base === 'light'
        rest: 1, haloPeak: 1             // behavior overrides
    }
});
```

### Runtime API

```js
lh.configure({ beamPeriod: 4 });        // live options apply immediately
lh.configure({ theme: 'light' });       // structural options rebuild in place,
                                        // preserving animation state
lh.getOptions();                        // copy of the resolved options
lh.setMode('static');                   // freeze / unfreeze ('rotate')
lh.start();
lh.destroy();                           // stop, remove listeners, clear the DOM
```

## Logo assets

`logo/` holds the canonical Metanorma logo files as PNG/SVG pairs, named
`metanorma-logo_{full|icon}-{light|dark|dark-bg|light-bg}[-old].{png,svg}`.
Treat every file there as source — never delete or overwrite (see `CLAUDE.md`).
