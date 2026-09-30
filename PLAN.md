# enc-chart-repo: the founding plan and running record

NOAA's **nautical charts**, for the map. Created on GitHub by the owner and given its documents by the site's
`pipeline/scaffold/new-origin.py`. **Its files are committed by hand under `map/` and published on dispatch.**

## What it is for

**The charts' land** (`map/noaa-land/`): the Electronic Navigational Charts' land areas (`LNDARE`), each place from the finest usage band that charts it, with the charts' coverage (`M_COVR`), and inside US waters, where no chart covers a place within 2 km of Natural Earth's land, that place as land. Zoom-8 Mapbox vector tiles (layers `land` and `cover`, extent 65536) under a version named by their own hash, and `noaa-land/index.json` naming the version and every tile. It is the land an ocean field is clipped at along US coasts. Committed by hand and published on dispatch; it moved here from `realtime-data-repo`'s statics on 2026-09-30. A chart layer or basemap is expected to follow.

## Where the data comes from

NOAA Office of Coast Survey, ENC Direct to GIS (`https://encdirect.noaa.gov/arcgis/rest/services/encdirect`): every usage band's land (`Land_Area`) and coverage (`enc_coverage`) layers, a U.S. government work in the public domain. **Read 2026-09-30**: 8 min 43 s to fetch every band into a cache; the coastal band 371 coverage polygons and 38,889 land polygons, the general 103 and 8,912, the overview 26 and 3,423. The merge runs by hand, with Shapely, from a generator kept in a private repository; nothing here runs it.

## Open

1. The first dispatched run, read: Pages and R2.
2. A chart layer or basemap, expected.
3. When no reader asks `realtime-data-repo` for its `noaa-land/` any more, remove it there.
