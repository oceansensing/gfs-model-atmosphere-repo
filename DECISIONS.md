# Decisions

Dated, irreversible-leaning decisions, one entry each, newest last. The
reasoning lives in `PLAN.md`.

**What counts as one-way in a data repository**: a decision that puts bytes in
readers' hands under a shape they will code against; a decision about which
repository owns a product, since moving one costs a migration in two places;
and a decision that forecloses an upstream.

## D1 — 2026-09-27 — Its own repository, published but not drawn

The GFS **atmosphere**, in a repository of its own under the convention every model
follows: **a model splits along the axis that costs bytes** — currents,
fields and, where the model has them, biogeochemistry — and an atmospheric
model has one atmosphere repository. See `espc-model-repo`'s `DECISIONS.md`
D2 for the measurement behind the split.

**Published but not drawn** (the owner, 2026-09-27): the products go to Pages
and R2 on a schedule and the website's map carries no layer for them, while
its status line reports their health. Drawing one later is a change to the
map, not to this repository.

One-way in the ordinary data-repository sense: moving a product between
repositories is cheap in machinery and expensive in everything that points at
it — roots in the contract, origins in the site's config, and the union
`check:docs` holds across origins.

## D2 — 2026-09-27 — GFS 0.25 degree, the step nearest now, global

One global grid per root on the lattice every global grid here uses, the hourly step nearest now from the newest posted cycle; published, not drawn.

## D3 — 2026-11-08 — To R2 alone, and the wind and air temperatures a day either side, remembered on R2

**Every product to the second host alone** (`r2_only`, the site pipeline's
D13): none is drawn on the website's map, so GitHub Pages carries this
origin's status and nothing else. **The 10 m wind and the 2 m and 850 hPa air
temperature a day either side, hourly**: each base lists in D31's `frames`
the next 24 hours of its cycle and the 24 behind that earlier runs published,
every other hour a file named for its time (`<root>.v<time>.json`), its
header saying its `lead`. About 980 MB with both days full — too much for the
`published` branch, force-pushed every hour — so those dated files are
remembered on R2 (`memory = "r2"`, the site pipeline's D15) and each run reads
them back first with a read-only token; the roots stay on the branch.

One-way in the ordinary sense: the dated files are a shape readers will code
against, and a product moved back to Pages would carry a gigabyte there.
