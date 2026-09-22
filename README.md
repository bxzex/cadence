# Cadence

Sing, play or load a melody and it writes the notes on a stave.

https://bxzex.github.io/cadence/

Pitch detection is YIN, with parabolic interpolation for sub-sample accuracy. The hard part turned out to be repeated notes, because the same pitch played twice looks like one long note. Cadence watches the level instead. A dip followed by a rise counts as a new note.

On test tones from C3 to C6 the worst error was 0.44 cents. The four built-in studies come back note for note. Ode to Joy used to merge its repeated notes, which is why that rule exists.

You can use the mic, a file or a built-in study. Audio stays in the page.
