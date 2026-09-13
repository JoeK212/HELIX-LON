# Helix-Lon

A 3D concept sketch: what if the Deci-Lon's log scales were wrapped helically
around a cylinder instead of drawn straight? Wrapping the scale gains you
real length — press **Unroll to compare length** to watch D straighten out
next to a plain reference bar and see the actual size difference, rather
than take a number's word for it. For D specifically, at this build's
chosen radius and turn count, that's **≈9.5×** the length of a straight
scale in the same vertical footprint — computed exactly from the helix's
geometry (arc length = √((2πRN)² + H²)), not estimated from turn count
alone. An earlier version of this README claimed "4 turns ≈ 4× the length,"
which undercounted by more than half — turn count alone ignores the
radius's own contribution to the actual unrolled length.

Eight scales, same relationships as the flat [Deci-Lon](../keuffel-esser-decilon)
tool:

- **D** (blue) — fixed reference scale, 1 to 10.
- **C** (red) — slides along the shared axis, same C/D multiply-divide
  relationship as the flat tool, just with height standing in for horizontal
  position.
- **A** (green) — fixed, reads x² relative to D at the same cursor height.
- **K** (amber) — fixed, reads x³ relative to D at the same cursor height.
- **LL** (purple, eˣ) — fixed, same double-log math as the flat tool's LL
  scales (t = log10(ln v)), covering roughly e to e¹⁰.
- **S** (cyan, sine) and **T** (pink, tangent) — fixed, read 10×sin(angle)
  or 10×tan(angle) against D, same convention as a real slide rule's S/T
  scales (decimal point tracked by you, as always).
- **L** (gray, linear) — fixed, the one non-logarithmic scale here.
  Reading it alongside D gives 10×log₁₀(D's value) — the piece a real
  slide rule uses to read a logarithm's value directly.

A translucent disk cursor, lit by a real point light that glows on whatever
it's near, slides along the axis and reads all eight scales at once.
Dragging the C helix also spins it, cosmetically — rotation around the
shared axis can't change a point's height, so it can't affect any reading;
it's there purely so the slide looks like threading a screw. A flat
reference strip mirrors the same numbers as plain straight lines, always
visible, and is itself draggable — it drives the same state the 3D view
does, not just a readout of it. Releasing a cursor drag near a whole D
value snaps to it exactly, with a quick pulse. Leave it alone for a few
seconds and the camera drifts slowly around on its own.

## Controls

- Drag the **red helix** (or the C row on the flat strip) up or down to
  slide it (multiply/divide).
- Drag the **white ring** (or anywhere else on the flat strip) up or down
  to move the cursor — or use the **arrow keys** (Shift for bigger steps).
- Drag the **background** to orbit the camera; scroll to zoom.
- **Turns** stepper (1–8) changes how many times the helix winds around —
  a real parameter, not a fixed constant. Rebuilds all eight scales and
  recomputes the length ratio from the new geometry; the readout values
  themselves never change, only the coil shape (turn count affects how the
  scale is drawn, never what it represents).
- **Copy link to this view** captures the exact cursor/slide position in
  the URL, so a specific setup can be shared directly.
- **Unroll to compare length** morphs D from its coiled helix into a
  straight line of its true arc length, with a short reference bar (the
  straight-scale footprint) alongside — free play only. Only D unrolls,
  not the other seven scales; one is enough to make the point, and C's
  slide-offset interaction doesn't have a meaningful analog once straight.
  The camera shot varies each time too — it inherits your current orbit
  angle and scales distance with the current arc length, rather than
  resetting to one fixed shot regardless of turns or where you were looking.
- **Export STL** downloads a binary STL of all eight scales — a real
  printable/millable object, not just a screen demo. D and C export in
  whatever pose they're actually in (D's coiled/unrolled state, C's slide
  position); the other six export at reduced resolution from the on-screen
  display geometry, since the full 900×8-segment smoothness is well past
  what a physical print or mill pass needs.
- **Quick Calculate** panel positions the slide and cursor for a range of
  presets:
  - *Basic:* a×b, a÷b, a², a³, √a, 1÷a, aᵇ
  - *Trig (degrees):* sin(a), cos(a), tan(a)
  - *Logs & growth:* log₁₀(a), ln(a), eᵃ, log_b(a)

  log_b(a) is the one preset that isn't read off a single scale — it needs
  two readings divided against each other, which no single cursor position
  can show, so it's computed and reported instead. Everything else is a
  genuine scale reading.

## How this compares to the real thing

The actual Fuller calculator (patented 1878, still sold nearly a century
later) doesn't work quite like this. It has one 50-turn helical scale —
about 500 inches unrolled — read by two independent pointers: a long cursor
that both slides along the axis and rotates freely, and a second pointer
fixed to the base. You set a number under the fixed pointer, then rotate and
slide the long cursor's pointer to a reference mark; multiplying is reading
where the same cursor pointer now lands relative to the helix after that
move. One scale, clever pointer geometry — not two interleaved scales.

Helix-Lon is a different, simpler design invented to reuse the flat
Deci-Lon's math directly: two separate coaxial helices (C and D) standing in
for the usual C/D pair, with height doing the job x-position does on a
straight rule. It's not a Fuller replica — it's what a Deci-Lon looks like
if you bend its scales into helices instead of straight lines. Worth being
upfront about, since the two are easy to conflate at a glance.

True calculus (derivatives, integrals) isn't and won't be represented — a
log-scale instrument computes by adding lengths that represent logarithms,
which gives multiplication, division, powers, roots, trig, and exponentials,
but not differentiation or integration. eˣ and ln(x) are the pieces of this
instrument that actually show up in calculus contexts (growth/decay, eˣ
being its own derivative), which is as close as an honest answer gets.

## Notes

Requires a tablet or desktop — orbiting and dragging a 3D scene genuinely
doesn't work on a phone-sized viewport, so below 759px width the app is
replaced with a message saying so, same convention and threshold used
across the rest of the tool suite (SPIRA is the reference implementation).
An iPad Mini (768px) already clears that threshold, so no tablet-sized
screen is affected, only phones. The render loop skips its per-frame work
entirely while blocked, rather than running against a hidden canvas.

The chrome (header, panel, buttons) has a light/dark toggle; the 3D viewport
itself stays dark regardless, the same way most 3D tools keep their render
viewport dark even when the surrounding app theme is light.

No true bloom/post-processing glow — that needs EffectComposer and
UnrealBloomPass, addon modules not in the core three.min.js bundle, so it
would mean extra CDN script dependencies this build doesn't otherwise have.
The cursor's glow comes from an actual point light instead, which gets a
similar effect with nothing extra to load.

Built single-file, no build step. Three.js loaded from cdnjs. See
`CHANGELOG.md` for the phase-offset, tick-density, mantissa, and interaction
lessons learned building this out — useful reading before adding a ninth
scale or a new interaction surface, since most of the hard-won fixes here
generalize.

Joe.K · [axisbim.io](https://axisbim.io)
