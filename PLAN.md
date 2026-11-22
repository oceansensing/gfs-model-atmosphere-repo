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

## 2026-11-21 — every product two days ahead and one behind, R2 keeping what a base lists (D4)

Every product `hours_ahead = 48`, `hours_behind = 24` and `memory = "r2-kept"`
(the site pipeline's D16), each `writes` naming its dated frames; the
workflow's read-back step and its read-only token gone; the step thirty
minutes. The wind's and air temperatures' `frames` list the day either side
they listed before, and every other hour is in `moreFrames`: theirs from 25 to
48 ahead, and every hour of the other four, their base among them. **A run
reads its last base's listing for what it has published**, so it asks NOAA for
the base's own hour and the hours its cycle had not given.

**Measured** the same afternoon. NOAA posts a cycle's hours out of order — of
each of four cycles' 209 indexes (11-20 18Z to 11-21 12Z), 54 to 68 were
posted before an earlier hour's; at 21:47 UTC the 18Z cycle had f019 to f038
and not f017 or f018 — so a cycle is taken once every hour of its day ahead
is posted, and its second day is listed as far as it is posted without a gap.
In those four and the 18Z, every hour to f048 was posted 3 h 58 min to
4 h 15 min after its cycle, 5 to 34 minutes after its f024: the run at 25 past
the fourth hour finds both days whole. **Rehearsed** through the orchestrator from the live `published`
branch, on a new cycle (18Z, base 22Z): 392 messages, 336.1 MB and 49 indexes
from the bucket, 4 min 41 s end to end, the contract green, 357 entries for R2
(2.0 GB), 350 dated frames left off the branch (39 MB). A second run on top of the first's output, an hour
on (base 23Z, the stage the first's branch alone): 16 messages, 13.8 MB and two
indexes, 21 s, 28 entries for R2 (157 MB), the base's hour read again byte for
byte what the first run sent — so its R2 publish, planned over the bucket the
first left, sends 24 files and keeps 402 hours, none dropped. Before, under D3:
an hour on 9 requests and 6.9 MB, a new cycle 92.5 MB for the three, and 159
files, 1,039.7 MB, read back from R2 every run (the run of 22:28 UTC that day).

## The workflow's packages come from the site — 2026-09-27

The publish workflow installs `site/scripts/requirements-gfs.txt`, one file
per fetcher family, instead of naming packages in its own `pip install`
line. Dependabot reads requirements files and never a workflow line: an
inline pin elsewhere had carried `requests` 2.32.3, a version with two
advisories, unflagged. The site's `check:docs` now refuses an inline package
here. Confirmed by a dispatched run, green on build, Pages and R2.

**Live since 2026-11-22**: run `44968278426` (00:46 UTC) the first on `a59f6ce`, green; the branch moved after R2
from run `44985216191` (04:28 UTC, D4 as amended).
