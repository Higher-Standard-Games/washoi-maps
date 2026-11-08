# Washoi maps

Sources for the maps Washoi ships, and the models they place, in the game's
path layout (`maps/`, `models/mapobjects/`). Compiling `maps/<id>.map` gives
`<id>.bsp` under its release name. Textures and shaders are not here: they come
from Warfork's media and the `washoi_textures.pk3` master.

| Map | Release | Origin |
| --- | --- | --- |
| `maps/washoi_dm1.map` | Washoi DM1 (Flew over) | warfork-maps `maps/wfdm1.map` |
| `maps/washoi_dm3.map` | Washoi DM3 (Deeper Underground) | warfork-maps `maps/wfdm3.map` |
| `maps/washoi_dm2.map` | Washoi DM2 (Le Dream On) | warfork-maps `wswmaps/wdm2.map` |
| `maps/washoi_dm5.map` | Washoi DM5 (viciious' lair) | warfork-maps `maps/wfdm5.map` |
| `maps/washoi_dm7.map` | Washoi DM7 (Crocinus bridge) | warfork-maps `maps/wfdm7.map` |
| `maps/washoi_dm11.map` | Washoi DM11 (Warehouse: C) | warfork-maps `maps/wfdm11.map` |
| `maps/washoi_dm14.map` | Washoi DM14 (Reflected) | warfork-maps `maps/wfdm14.map` |
| `maps/washoi_amphi1.map` | Washoi Amphi1 | warfork-maps `wswmaps/wamphi1.map` |
| `maps/washoi_snd1.map` | Concrete Strike | warfork-maps `maps/wfbomb1.map` |
| `maps/washoi_amphi2.map` | Washoi Amphi2 (Octagon Obsession) | warfork-maps `wswmaps/wda5.map`, corrected |
| `maps/washoi_snd6.map` | Depot | warfork-maps `wswmaps/wbomb6.map`, corrected |
| `maps/washoi_snd4.map` | Shepas | warfork-maps `maps/wfbomb4.map`, with `_lightmapImageSize 2048` and `gridsize 64 64 64` |
| `maps/washoi_dm12.map` | Washoi DM12 (Courtyard) | warfork-maps `wswmaps/courtyard/wdm12.map`, corrected |

Original import warfork-maps revision: `00bf74a72c6a66561e07571c59b4ca99850279fa`.
DM2, DM11, DM14, Amphi1 and S&D1 retain their initial imported sources.
The served BSPs of DM11, DM14 and S&D1 are Jal's builds; DM2 and Amphi1 use
their original compiled builds. The November refresh below records the sources
and compiled builds for DM1, DM3, DM5 and DM7.

## Corrections in amphi2, snd6 and dm12

These three were compiled here, with the MakeBSP in `shag/tools/makebsp`
(`-game washoi -samplesize 4 -lightmapimagesize 2048`, then MakeLight).

- **Collision.** They were made for q3map2, where a placed model has no
  collision unless its `spawnflags` include 2; the mapper's clip brushes do the
  rest. MakeBSP makes every model solid, and its convex hulls fill open space
  (the pipes over Amphi2's tower jump pad closed the shaft). Every `misc_model`
  without spawnflag 2 has `"collisiontype" "none"`, which restores the original
  collision: the clip brushes are the same 334 fullclip and 69 playerclip
  brushes as Warsow's 2015 Depot build. In dm12, 165 models have no collision;
  its 232 fullclip and 146 playerclip brushes do the rest. Its 9 solid models
  have `"collisiontype" "extrude"`, MakeBSP's per-polygon collision, as q3map2
  clipped a solid model's triangles: the default convex hull of the curved
  ceiling closed the shaft above the jump pad by the Mega Health.
- **Worldspawn.** `_lightmapImageSize 2048` and `gridsize 64 64 64`, as in Jal's builds.
- **Material names.** amphi2: `refly/Bricks_Refly_DarkGrey1` →
  `refly_bricks/Bricks_Refly_DarkGrey1` (69 faces). snd6: one visible
  `dev/vertical_orange` end cap → `exwsw/eX_rplates_01`.
- **Models.** `wda5/wda5_BlueSmallSign.ase` names `textures/billboard/bulletsblue2`
  (was `billboard_001/…`); `city/light_street_2way_2.ase` names `halo_large`
  (was `textures/halo_large`). Amphi2's slim neon advert is
  `wda5/wda5_washoi_neon.ase`, a copy of `wsw_adverts/tech_add_1_b.ase` whose
  sign shows the whole of `textures/billboard/neon1_tall`.

The `.map` sources of dm12's courtyard models sit beside them in
`models/mapobjects/courtyard/`.

## Models from elsewhere

`SOURCES.json` lists how many files came from each source. Files not in
warfork-maps:

| File | From |
| --- | --- |
| `models/mapobjects/wda5/wda5_WallPipe.ase` | `rapid.tar` (2013) |
| `models/mapobjects/crates/crate_wood.ase` | `rapid.tar`; Warfork ships `crate_wood.obj` |
| `models/mapobjects/decor_misc/airshaft.ase` | `rapid.tar`; Warfork ships `airshaft.obj` |

`washoi_snd1.map` names `handrails/handrail_2.ase`, which exists nowhere;
`handrail_2.obj` is its Warfork counterpart (the wfbomb1 compile used it).

## November map refresh

DM1, DM3, DM5 and DM7 use warfork-maps revision `4067818bb3225062a389eafa49819bcb8fe21dae`.
Their map and referenced model sources are copied without edits; the existing
`airshaft.ase` fallback remains available for DM5. The per-file import ledger is
`imports/beta8-map-packages.json`. The runtime BSPs come from warfork-qfusion
`assets/data1_21pure/maps/wfdm{1,3,5,7}.bsp`, under their Washoi release names.
