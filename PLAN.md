# enc-chart-repo: the founding plan and running record

NOAA's **nautical charts**, for the map. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Its files are made by the site's generator, run by this repository's generate workflow, committed only when they change and published by the same run** — monthly, on the 2nd at 07:23 UTC, and on dispatch.

## What it is for

**The charts' land** (`map/noaa-land/`): the Electronic Navigational Charts' land areas (`LNDARE`), each place from the finest usage band that charts it, with the charts' coverage (`M_COVR`), and inside US waters, where no chart covers a place within 2 km of Natural Earth's land, that place as land. Zoom-8 Mapbox vector tiles (layers `land` and `cover`, extent 65536) under a version named by their own hash, and `noaa-land/index.json` naming the version and every tile. It is the land an ocean field is clipped at along US coasts. Made by the site's generator and published by this repository's generate workflow; it moved here from `realtime-data-repo`'s statics on 2026-09-30. A chart layer or basemap is expected to follow.

## Where the data comes from

NOAA Office of Coast Survey, ENC Direct to GIS (`https://encdirect.noaa.gov/arcgis/rest/services/encdirect`): every usage band's land (`Land_Area`) and coverage (`enc_coverage`) layers, a U.S. government work in the public domain. **Read 2026-09-30**: 8 min 43 s to fetch every band into a cache; the coastal band 371 coverage polygons and 38,889 land polygons, the general 103 and 8,912, the overview 26 and 3,423. The merge runs with Shapely, from a generator kept in a private repository (the site's), which this repository's generate workflow runs: it fetches the charts afresh, writes this land and `river-data-repo`'s rivers together, and **a guard stops a run whose drawn land moves more than 50 km² in one tile or 250 km² in all, or whose coverage moves more than 5,000 km²**, naming the tiles for a person to look at first; a dispatch with `accept` lets a looked-at run through.

## Open

1. The first dispatched run, read: Pages and R2.
2. A chart layer or basemap, expected.
3. When no reader asks `realtime-data-repo` for its `noaa-land/` any more, remove it there.

## Record

**2026-09-30.** First publish, run `36751209681`: `noaa-land/` version
`012b39a3e7` (950 zoom-8 tiles, 18.8 MB), build, Pages and R2 green; listed in
the site's `MAP_ORIGINS` after it. **Open**: a square only the general band
covers (`US2EC03M`, about 1:600,000, east of the uncharted square in the
Rappahannock at 37°44.6′–37°48′ N) keeps that chart's generalized river, a
rectangle of water over the south bank.

**Decided 2026-09-30, to build next**: the generator moves into the site's
pipeline, and a `generate.yml` here runs it monthly and on dispatch,
committing this land and `river-data-repo`'s rivers together only when they
changed, with a guard that stops a run whose changes pass a threshold.
**Open**: whether USGS decides squares only a small-scale chart covers (the
one above) — its first run was held unpublished.

**2026-09-30, evening.** The generator moved into the site's pipeline and
the generate workflow joined this repository. Its first dispatched run,
`36775880609` (47 min: the charts fetched afresh, USGS asked three at a
time), wrote `noaa-land/` `ea33a419d7` — NOAA's updates since the morning,
the largest 0.03 km² of drawn land — and `river-data-repo`'s rivers
`d71c8d904e`; its guard read 81.9 km² of drawn land moved in all and 47.1 in
the largest tile, within its limits; both publishes green (`36781095136`
here, `36781091333` there). Its schedule is on since: monthly, the 2nd.
The rectangle over the Rappahannock's south bank is closed by the rivers
(below, and `river-data-repo`'s record).

