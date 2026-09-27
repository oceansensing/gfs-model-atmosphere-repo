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
