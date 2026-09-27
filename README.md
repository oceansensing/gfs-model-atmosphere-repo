# gfs-model-atmosphere-repo

The GFS **atmosphere** — a data repository of the oceansensing ocean map system: its own
Pages site, its own schedule, its own gigabyte, holding no code of its own.

**Built, rehearsed and taken live 2026-09-27** — published to Pages and R2,
not drawn on the website's map. `PLAN.md` is the founding plan;
`CLAUDE.md` carries what must not be got wrong and the shared doc doctrine.

## What it publishes

NOAA's Global Forecast System at 0.25°: near-surface wind, air
temperature and the other atmospheric fields the ECMWF layers already carry,
as a second opinion beside them.

| root | quantity | unit |
| --- | --- | --- |
| `wind-gfs.json` | 10 m wind, a vector pair | m s-1 (integers at 0.01) |
| `air-gfs.json` | 2 m air temperature | degC |
| `air850-gfs.json` | 850 hPa air temperature | degC |
| `mslp-gfs.json` | sea-level pressure | hPa |
| `hgt500-gfs.json` | 500 hPa geopotential height | gpm |
| `cloud-gfs.json` | total cloud cover, instantaneous | fraction |
| `prate-gfs.json` | precipitation rate, instantaneous | mm/h |

Global, 1440 x 721 from 90 N and 0 E; 41 MB a tree (measured 2026-09-27).

These products are published **operationally but not drawn on the website's
map** — the owner's call, 2026-09-27. The map's status line still reports
them when they fall behind, which is how their health stays visible.

## Where the data comes from

**Source**: NOAA's open-data bucket on AWS, registry entry
<https://registry.opendata.aws/noaa-gfs-bdp-pds/>, GRIB2 read by byte range
through each file's `.idx`. The study of its layout and latency is this
repository's first PLAN entry, written when the fetcher is.

## How it will run

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository will carry `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Sibling repositories of the same model:
none — an atmospheric model has no currents/fields split.

**Which document gets what, and what "update docs" means across all
twenty repositories, is the doctrine block at the top of `CLAUDE.md`** —
the same text in all twenty, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
```
