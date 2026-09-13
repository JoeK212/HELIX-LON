# Helix-Lon

A 3D concept sketch: the Deci-Lon's log scales wrapped helically around a
cylinder instead of drawn straight, gaining real length over a straight
rule in the same footprint — press **Unroll to compare length** to see it
(≈9.5× for D, computed exactly from the helix geometry, not estimated from
turn count).

Eight scales, same relationships as the flat [Deci-Lon](../keuffel-esser-decilon):

- **D** (blue) — fixed reference, 1–10
- **C** (red) — slides along the axis; C/D multiply-divide
- **A** / **K** (green/amber) — fixed, x²/x³ relative to D
- **LL** (purple, eˣ) — fixed, double-log, roughly e to e¹⁰
- **S** / **T** (cyan/pink) — fixed, 10×sin/10×tan against D
- **L** (gray, linear) — the one non-log scale; reads 10×log₁₀(D)

A lit disk cursor reads all eight at once. A flat reference strip mirrors
the same numbers as plain straight lines and drives the same state as the
3D view. Cursor drags near a whole D value snap to it. Camera drifts slowly
when idle.

## Controls

- Drag the **red helix** (or C row on the flat strip) to slide (multiply/divide)
- Drag the **white ring** (or elsewhere on the strip) to move the cursor,
  or use **arrow keys** (Shift = bigger steps)
- Drag background to orbit, scroll to zoom
- **Turns** (1–8) — live parameter; rebuilds all scales and the length
  ratio, readout values never change
- **Copy link to this view** — shares the exact cursor/slide position
- **Unroll to compare length** — straightens D next to a reference bar
  (free play only; D only)
- **Export STL** — binary STL of all eight scales, printable/millable
- **Quick Calculate** — presets for a×b, a÷b, a², a³, √a, 1÷a, aᵇ, sin/cos/tan(a),
  log₁₀(a), ln(a), eᵃ, log_b(a)

## vs. the real Fuller calculator

The actual Fuller calculator (1878) is one 50-turn helical scale read by two
independent pointers — not two interleaved scales. Helix-Lon reuses the flat
Deci-Lon's math instead: two coaxial helices (C and D) standing in for the
usual pair, height doing the job x-position does on a straight rule. Not a
replica. And like any log-scale instrument, it covers multiplication,
division, powers, roots, trig, and exponentials — not calculus.

## Notes

Requires a tablet or desktop (blocked below 759px — orbiting/dragging 3D
doesn't work on phone-sized viewports). Chrome has a light/dark toggle; the
3D viewport stays dark either way. Cursor glow is a real point light, not
post-processing bloom (keeps this a single-file, no-build-step app —
three.js loaded from cdnjs, nothing else).

See `CHANGELOG.md` for the phase-offset, tick-density, mantissa, and
interaction lessons learned building this — worth a read before adding a
ninth scale or new interaction surface.

Joe.K · [axisbim.io](https://axisbim.io)
