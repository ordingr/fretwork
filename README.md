# Fretwork

An interactive guitar fretboard for practising **three-note-per-string** scales — plus a matching piano keyboard and a live circle of fifths, so you can see the same seven notes three ways at once.

One self-contained HTML file. No build step, no dependencies, no backend.

![Fretwork](docs/screenshot.png)

## What it does

**Fretboard** — 22 frets, six or seven strings, drawn with true scale-length fret taper. Dots are coloured by function: root, third, fifth, other scale tones. Notes outside the current position show as dashed ghosts so you can see where to shift next. When a chord is in force, tones it needs that the scale does not have are drawn as bone-white rings — the G♯ in an E major over A minor, which is exactly the note that makes it a V rather than a v.

**3NPS positions** — one position per scale degree, each labelled with the note it starts on and its fret range. Switch to 2 notes per string for pentatonic boxes, or 4 for stretch work.

**Piano** — two octaves, C3 to C5, and it looks like a piano: white naturals, black accidentals, always. Scale function is carried by a coloured band under each key rather than by repainting it. Red discs mark the chord **as it is actually voiced**, so switching between root position, 1st, 2nd and 3rd inversion shows the notes physically move, and each disc is numbered with the order the comping pattern strikes it — notes hit together share a number. As the loop runs, each key lights the moment it sounds, so an arpeggio is something you watch, not just hear. **Keyboard shows** filters to all keys, the scale, or the position you're drilling.

**Circle of fifths** — the scale's notes are highlighted in place, so you can see that a major scale is seven *adjacent* slices of the circle and that harmonic minor isn't. Reports the key signature, derived from the scale's own spelling. Click either ring to jump key.

**Chords** — the seven chords the current scale generates, stacked in thirds through the scale itself, as triads or sevenths with Roman numerals. Every mode gets its own set, and it stays correct in the awkward corners: A harmonic minor yields Am(maj7), Bm7♭5, Cmaj7♯5, Dm7, E7, Fmaj7, G♯°7. Click a chord to hear it and light its tones on the neck.

**Progressions** — ii–V–I, 12-bar blues (straight and quick-change), I–V–vi–IV, the andalusian cadence, the full diatonic circle and more. Pick one and it loops in time as a backing track, so you can solo over it with the shape you're drilling. While it plays, everything that isn't a chord tone *right now* fades back on both the fretboard and the piano — target-note practice.

**Feel, metre and voicing** — nine comping styles (block, pad, strum, bass-and-chord, waltz, charleston, arpeggio up, arpeggio up-and-down, Alberti bass) against 2/4, 3/4, 4/4, 5/4, 6/8 or 12/8, all following the same tempo control. The compound signatures count the dotted quarter, so 6/8 at 200 BPM gives a 0.6-second bar rather than a 1.8-second one. Inversion is fixed or **Smooth**, which picks the inversion that moves least from the previous chord — ordinary voice leading, and it makes the loop sound like music instead of a chord chart.

Each progression is also drawn on the circle of fifths as root motion. ii–V–I is three adjacent slices stepping anticlockwise; the diatonic circle is a full loop with one long diagonal across it, the tritone jump where the key runs out of perfect fifths.

**Playback** — plays the position with a Karplus–Strong plucked-string voice, following each note on both instruments. **Pattern** switches between running the scale and running the **arpeggio** of whatever chord is in force — and if a progression is looping, the arpeggio follows it, restarting from the bottom on each chord. Scales without a stack of thirds still get one: a tonic chord is derived from the scale's own degrees, so minor pentatonic arpeggiates Am and whole tone arpeggiates A+. 40–220 BPM, quarters/eighths/triplets/sixteenths, up / down / up-and-down, loop, metronome. Click any dot or key to hear it alone.

**20 scales** — all seven major modes, harmonic and melodic minor, phrygian dominant, lydian dominant, altered, both pentatonics, minor and major blues, whole tone, both diminished scales, and chromatic.

**Chromatic mode** switches to the exercise people actually practise: a four-fret window on every string, one finger per fret, movable up the neck.

**Tunings** — standard, drop D, E♭/D standard, DADGAD, open G, open D, 7-string. Left-handed toggle.

Keyboard: <kbd>Space</kbd> play/stop · <kbd>←</kbd><kbd>→</kbd> position · <kbd>↑</kbd><kbd>↓</kbd> tempo.

## How the shapes are generated

Nothing is hard-coded. A position is built by walking the scale upward in pitch from its starting degree — each note's MIDI number is the previous one plus the next interval in the scale — then assigning notes to strings `n` at a time and converting to frets against the open-string pitches. Because the pitches are exact, only the octave of the whole shape is ever adjusted to fit the neck, and alternate tunings and seven-string necks stay correct for free.

Note names are spelled properly per key rather than picked from a chromatic list: each scale degree takes its own letter, with the accidental derived from the pitch class. F♯ lydian gives you A♯ and B♯, not B♭ and C.

Verified against the standard fingerings — C major position 1 comes out `8·10·12 / 8·10·12 / 9·10·12 / 9·10·12 / 10·12·13 / 10·12·13`, and A minor pentatonic at 2 notes per string reproduces the familiar boxes 1 and 2.

## Running it

Open `index.html` in a browser. That's the whole thing.

To serve it — for phones on your network, or behind a tunnel:

```bash
docker compose up -d
# http://localhost:3094
```

The only network request the page makes is the Google Fonts stylesheet; without it the page falls back to system fonts and everything still works.

## Licence

MIT — see [LICENSE](LICENSE).
