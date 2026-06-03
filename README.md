# Selbsthemmung durch Verkanten — interaktiv

An interactive, dependency-free visualization of **self-locking by canting**
(*Selbsthemmung durch Verkanten*): a loose sleeve on a fixed shaft is loaded on a
lever arm, cants, and pinches the shaft at two diagonal contacts. Each contact has
a **friction cone** (Reibungskegel); the clamp holds as long as the reaction stays
inside its cone.

Single static `index.html` — vanilla JS + `<canvas>`, no build step, no framework.
Light/dark theming follows the OS preference.

## The physics

Driving the analysis is the friction angle **ρ = arctan(μ)** and the angle the
reaction must lean from the contact normal, **β = arctan(h / 2a)**.

- **Self-locking when** `β ≤ ρ`, i.e. **`a ≥ h / (2μ)`**.
- The shaft **diameter** spreads the two contacts (and their cones) apart but
  drops out of the locking threshold — the upper cone edges always cross at
  `x = h/(2μ)` from the shaft axis, regardless of diameter. It is fixed at 5 mm
  in the drawing (visual only).
- The result is independent of the load magnitude, which is the hallmark of
  self-locking: grip scales with the load it has to resist.

## Parameters

| Control | Meaning | Range |
| --- | --- | --- |
| `a` | load distance / lever arm (mm) | 5–80 |
| `h` | distance between contact points / *Abstand Kontaktpunkte* (mm) | 5–120 |
| `μ` | friction coefficient | 0.05–0.6 |

The shaft diameter is fixed at 5 mm and only affects the drawing, not the
locking condition.

## Interacting

- **Live banner & metrics** show whether the clamp holds (`β ≤ ρ`) or slips,
  plus the condition `a/h ≥ 1/(2μ)`.
- **Hover (or focus) a slider** to overlay a technical-drawing dimension of that
  parameter on the canvas — a linear dimension for `a` and `h`, an angular
  dimension (friction cone ρ) for `μ`.
- **Reibpaarung dropdown** offers typical material pairings (e.g. Stahl–Stahl,
  Stahl–Aluminium, Aluminium–Aluminium). Picking one sets `μ`; moving the `μ`
  slider snaps the dropdown back to the matching pairing or to *benutzerdefiniert*.
  The listed coefficients are representative static-friction (Haftreibung) values
  and vary with surface finish and lubrication.

## Run locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy (GitHub Pages)

1. Push this folder to the repository.
2. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch**.
3. Branch `main`, folder `/ (root)`. The site goes live at
   `https://<user>.github.io/<repo>/`.

> Note: GitHub Pages serves content publicly even from a private repository's Pages
> site. Keep that in mind if the repo is private for confidentiality reasons.

## License

MIT (or adjust to taste).
