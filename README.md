# Selbsthemmung durch Verkanten — interaktiv

Interactive, dependency-free visualizations of **self-locking by canting**
(*Selbsthemmung durch Verkanten*) — vanilla JS + `<canvas>`, no build step, no
framework. Light/dark theming follows the OS preference.

Two demos behind a landing page, each available in two languages (switcher in
the top-right corner):

| Page | English | Deutsch |
| --- | --- | --- |
| **Landing page** — pick a scenario | [`index.html`](index.html) | [`index.de.html`](index.de.html) |
| **Part I — Sleeve on a shaft**: a loose sleeve on a fixed shaft is loaded on a lever arm, cants, and pinches the shaft at two diagonal contacts | [`sleeve.html`](sleeve.html) | [`sleeve.de.html`](sleeve.de.html) |
| **Part II — Tilted plate on a rod**: a sheet with a clearance hole cants on a rod; the diameters set the tilt angle and contact distance | [`plate.html`](plate.html) | [`plate.de.html`](plate.de.html) |

All pages are self-contained; each language pair shares identical physics and
interaction code. Every demo page links back to the overview and to its sibling
demo.

## The physics

### Part I — sleeve on a shaft

Driving the analysis is the friction angle **ρ = arctan(μ)** and the angle the
reaction must lean from the contact normal, **β = arctan(h / 2a)**.

- **Self-locking when** `β ≤ ρ`, i.e. **`a ≥ h / (2μ)`**.
- The shaft **diameter** spreads the two contacts (and their cones) apart but
  drops out of the locking threshold — the upper cone edges always cross at
  `x = h/(2μ)` from the shaft axis, regardless of diameter. It is fixed at 5 mm
  in the drawing (visual only).
- The result is independent of the load magnitude, which is the hallmark of
  self-locking: grip scales with the load it has to resist.

### Part II — tilted plate on a rod

A sheet of thickness `t` with a clearance hole of diameter `D` sits on a rod of
diameter `d` and is pushed parallel to the rod at distance `a` from the rod axis.
It tilts until both hole edges touch the rod at two diagonal contacts:

- **Tilt angle θ** from the clearance: `D·cosθ − t·sinθ = d`.
- **Contact distance** (along the rod): `w = D·sinθ + t·cosθ` — at zero
  clearance (`D = d`) this degenerates to `w = t`.
- **Self-locking when** `a ≥ w / (2μ)` — the same condition as Part I with `w`
  taking the role of `h`. The diameters enter the condition *only* through `w`:
  small clearance and a thin sheet give a small `w`, so the plate jams even for
  a force applied close to the rod.

## Parameters

### Part I (`sleeve.html`)

| Control | Meaning | Range |
| --- | --- | --- |
| `a` | load distance / lever arm (mm) | 5–80 |
| `h` | distance between contact points / *Abstand Kontaktpunkte* (mm) | 5–120 |
| `μ` | friction coefficient | 0.05–0.6 |

The shaft diameter is fixed at 5 mm and only affects the drawing, not the
locking condition.

### Part II (`plate.html`)

| Control | Meaning | Range |
| --- | --- | --- |
| `d` | rod diameter / *Stangendurchmesser* (mm) | 4–20 |
| `D` | hole diameter / *Lochdurchmesser* (mm) | 4.5–24 |
| `t` | sheet thickness / *Blechdicke* (mm) | 2–16 |
| `a` | load distance from rod axis (mm) | 5–80 |
| `μ` | friction coefficient | 0.05–0.6 |

`d` and `D` are coupled so the rod always fits the hole (`D ≥ d + 0.5 mm`);
moving one slider past the other drags it along. The tilt angle `θ` and contact
distance `w` are derived quantities, shown as metric cards and as an always-on
dimension in the drawing.

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
