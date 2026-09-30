# enc-chart-repo

NOAA's **nautical charts**, for the map: a data repository of the oceansensing ocean map system, with its own
Pages site, its own schedule and its own gigabyte, and no code of its own.

**Its files are committed by hand under `map/` and published on dispatch.** `PLAN.md` is the founding plan; `CLAUDE.md` carries what must not be
got wrong and the shared doc doctrine.

## What it publishes

**The charts' land** (`map/noaa-land/`): the Electronic Navigational Charts' land areas (`LNDARE`), each place from the finest usage band that charts it, with the charts' coverage (`M_COVR`), and inside US waters, where no chart covers a place within 2 km of Natural Earth's land, that place as land. Zoom-8 Mapbox vector tiles (layers `land` and `cover`, extent 65536) under a version named by their own hash, and `noaa-land/index.json` naming the version and every tile. It is the land an ocean field is clipped at along US coasts. Committed by hand and published on dispatch; it moved here from `realtime-data-repo`'s statics on 2026-09-30. A chart layer or basemap is expected to follow.

These products are published **operationally but not drawn on the website's map**; the map's status
line still reports them when they fall behind, which is how their health stays visible.

## Where the data comes from

NOAA Office of Coast Survey, ENC Direct to GIS (`https://encdirect.noaa.gov/arcgis/rest/services/encdirect`): every usage band's land (`Land_Area`) and coverage (`enc_coverage`) layers, a U.S. government work in the public domain. **Read 2026-09-30**: 8 min 43 s to fetch every band into a cache; the coastal band 371 coverage polygons and 38,889 land polygons, the general 103 and 8,912, the overview 26 and 3,423. The merge runs by hand, with Shapely, from a generator kept in a private repository; nothing here runs it.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Related repositories: `river-data-repo`, whose rivers are cut to fit this land, and `realtime-data-repo`, whose `map/noaa-land/` is the set this one replaced, kept while older readers still ask for it.

**Which document gets what, and what "update docs" means across all
twenty-four repositories, is the doctrine block at the top of `CLAUDE.md`**: the
same text in all twenty-four, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
map/            the committed files, published as they are
.github/        the publish workflow
```
