# Cadence

Pitch detection to written notation. The YIN algorithm follows a melody frame by
frame, groups what it hears into notes, and sets them on a stave.

Live: https://bxzex.github.io/cadence/

## How it listens

**YIN**, properly. The squared difference function, then the cumulative mean
normalised difference — which is the part that stops a detector locking onto
lag zero or dropping an octave — then the first lag under an absolute threshold
that is also a local minimum, then parabolic interpolation through the three
samples around it for sub-sample resolution.

**Segmentation** with hysteresis. A change of pitch ends a note immediately; a
few unvoiced frames are tolerated so one bad frame cannot split a sustained
note. Repeated notes are the hard case: the same pitch played twice is two
notes, not one, and the only clue is the level falling away and climbing back.
Cadence tracks each note's peak and treats a dip below 30% followed by a return
as a re-articulation.

**Quantisation** to a beat grid at a tempo you set, and a stave that draws
ledger lines, accidentals, stem direction by position, and hollow heads for
anything two beats or longer. The treble clef is a bézier path, not a font
glyph.

Microphone, an audio file, or one of four built-in studies.

## Verification

Both halves are checked against ground truth rather than by ear.

**The detector**: eight harmonic-rich tones at exactly known frequencies from
C3 to C6. Worst error is **0.44 cents**, and most are within 0.02.

**The transcription**: each study is synthesised from a known list of MIDI
notes, so the written output can be compared to what was actually played. All
four studies come back as an **exact match**, note for note — including Ode to
Joy, which has five repeated-note pairs and originally merged them. That failure
is what the re-articulation rule above was written to fix.

## Notes

One HTML file. No libraries, no build step. Audio is decoded locally and never
uploaded; the microphone stream never leaves the page.

Built by [bxzex](https://bxzex.com).
