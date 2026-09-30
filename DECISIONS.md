# Decisions

Dated, irreversible-leaning decisions, one entry each, newest last. The
reasoning lives in `PLAN.md`.

**What counts as one-way in a data repository**: a decision that puts bytes in
readers' hands under a shape they will code against; a decision about which
repository owns a product, since moving one costs a migration in two places;
and a decision that forecloses an upstream.

## D1 — 2026-09-30 — Its own repository, committed by hand and published on dispatch

The charts' land moved here from `realtime-data-repo`'s statics (the owner, 2026-09-30), with the rivers that open its uncharted squares in `river-data-repo` beside it. **Published on dispatch, never on a schedule**: the generator runs by hand, rarely, and a scheduled run would republish the same tree. One-way in the ordinary data-repository sense: moving the files again costs a reader's routing and a migration in two places.
