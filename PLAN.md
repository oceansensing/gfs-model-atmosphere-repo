# gfs-model-atmosphere-repo — the founding plan and running record

The GFS **atmosphere**. Created on GitHub by the owner and given its documents on
2026-09-27, the day the owner asked for ECCOFS, CBEFS, Mercator's
biogeochemistry, RTOFS and GFS to be published without the map drawing them.
**Built 2026-09-27.**

## What it is for

NOAA's Global Forecast System at 0.25°: near-surface wind, air
temperature and the other atmospheric fields the ECMWF layers already carry,
as a second opinion beside them.

## Where the data comes from

**Source**: NOAA's open-data bucket on AWS, registry entry
<https://registry.opendata.aws/noaa-gfs-bdp-pds/>, GRIB2 read by byte range
through each file's `.idx`. The study of its layout and latency is this
repository's first PLAN entry, written when the fetcher is.

## Open, as founded

*Answered 2026-09-27 — the entry below.*

## 2026-09-27 — built and rehearsed

The fetcher is the site's `scripts/fetch-gfs.py`; "What must not be got wrong" in
CLAUDE has its traps, each found on the first live run. Rehearsed through
the orchestrator in a throwaway copy of the site with the roots in its
contract: every file matched and every fate was `fresh`.

## 2026-09-27 — live

The site's commit `f872402` put the roots in the contract and the origin in
`MAP_ORIGINS`; the dispatched run 36297619942 went green on its first try (build,
Pages and R2), and `status/status.json` read at 2026-09-27T05:36:15Z: every
product `fresh` (7 of 7), the nearest frame 0.4 h
from the reader. The schedule `25 * * * *` was then turned on (longest gap
1 h, so the watchdog's silence budget is 3 h).

## 2026-11-08 — R2 alone, and three products a day either side (D3)

Every product `r2_only`; the wind and the two air temperatures list the next
24 hours of their cycle and the 24 behind, hourly, their dated files
remembered on R2 rather than on the branch (`memory = "r2"`) and read back by
the workflow's new first step with a read-only token
(`R2_READ_ACCESS_KEY_ID`, `R2_READ_SECRET_ACCESS_KEY`). **Measured** on a
sample against the bucket (the 12Z cycle): a run an hour on reads the one hour
entering the day, 9 requests and 6.9 MB — what a run reads today — and a new
cycle reads its 25, 129 requests and 92.5 MB, four times a day. Files 9.1,
5.3 and 5.3 MB an hour; about 980 MB with both days full.

## The workflow's packages come from the site — 2026-09-27

The publish workflow installs `site/scripts/requirements-gfs.txt`, one file
per fetcher family, instead of naming packages in its own `pip install`
line. Dependabot reads requirements files and never a workflow line: an
inline pin elsewhere had carried `requests` 2.32.3, a version with two
advisories, unflagged. The site's `check:docs` now refuses an inline package
here. Confirmed by a dispatched run, green on build, Pages and R2.
