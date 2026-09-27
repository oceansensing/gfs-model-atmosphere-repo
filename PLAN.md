# gfs-model-atmosphere-repo — the founding plan and running record

The GFS **atmosphere**. Created on GitHub by the owner and given its documents on
2026-09-27, the day the owner asked for ECCOFS, CBEFS, Mercator's
biogeochemistry, RTOFS and GFS to be published without the map drawing them.
**Nothing is published yet.**

## What it is for

NOAA's Global Forecast System at 0.25°: near-surface wind, air
temperature and the other atmospheric fields the ECMWF layers already carry,
as a second opinion beside them.

## Where the data comes from

**Source**: NOAA's open-data bucket on AWS, registry entry
<https://registry.opendata.aws/noaa-gfs-bdp-pds/>, GRIB2 read by byte range
through each file's `.idx`. The study of its layout and latency is this
repository's first PLAN entry, written when the fetcher is.

## Open

1. The fetcher, in the site's `scripts/`, and its self-test.
2. `pipeline/products.toml`, declaring only roots the site's contract
   publishes.
3. The publish workflow, its schedule offset from the siblings', and each
   product's `max_age_hours` measured from when the data really arrives.
4. The secrets only the owner can add: `PIPELINES_SSH_KEY` and the three
   `R2_*` organization secrets.
