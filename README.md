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
| `maps/washoi_dm16.map` | Washoi DM16 (The Deepest Underground) | warfork-maps `wswmaps/wdm16.map`, corrected |
| `maps/washoi_dm17.map` | Washoi DM17 (Le Toxiquet) | warfork-maps `wswmaps/wdm17.map`, corrected |
| `maps/washoi_dm18.map` | Washoi DM18 (Praxtor) | warfork-maps `wswmaps/wdm18.map`, corrected |
| `maps/washoi_amphi3.map` | Washoi Amphi3 (Melee) | warfork-maps `wswmaps/wda2.map`, corrected |

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

## Corrections in dm16, dm17, dm18 and amphi3

Compiled with the MakeBSP in `shag/tools/makebsp` from warfork-maps
`4067818bb3225062a389eafa49819bcb8fe21dae` (`-game washoi -samplesize 4
-lightmapimagesize 2048`, then MakeLight). Warfork's own `wfdm16`-`wfdm18` and
`wfda2` BSPs are 2015 q3map2 builds that predate the 2026 model updates.

- **Collision.** As in amphi2 and dm12: every `misc_model` without spawnflag 2
  has `"collisiontype" "none"`, and the solid ones (handrails, wdm17's
  doorway, wdm16's rock roof and wall pieces) have `"collisiontype" "extrude"`,
  so a convex hull never closes a doorway.
  dm16's five handrails are the exception: they are flat sheets, and `extrude`
  pushed each side's prisms out through the other, leaving an invisible ledge
  beside every rail. They use MakeBSP's default solid collision instead, and
  the playerclip that wrapped the rail at (1264, -1056) is removed.
- **Teleporters.** warfork-maps' 2026 `teleporter_01_b.obj` has its base 10.2
  units below its origin; the old model's was at the origin, and the maps still
  place it for the old one. dm16's two and dm17's four are raised 10.2 units,
  so they stand on the floor as in Warfork's own builds. dm17's four `extrude`
  handrails use the default solid collision as well (they are fully covered by
  the map's own clips, so collision is unchanged).
- **Worldspawn.** `_lightmapImageSize 2048` and `gridsize 64 64 64`. MakeLight
  has no `_floodlight`: each map's floodlight became `"ambient" "6"` with the
  floodlight's colour as `_color` (macro-occlusion ambient). dm18's original
  `ambient 5` with a blue `_color` is replaced by its orange floodlight colour, with `ambient 24`, `_lightingIntensity 2.5`, `radiosity 0.5` and no `_extradist` on its lights. dm16's lights have no `_extradist` either.
- **Texture scales.** warfork-qfusion replaced some images with larger ones in
  2026 without changing the maps, and a standard-format face's scale is in
  image pixels. Faces using them have scale divided and shift multiplied by the
  upscale: `decals/decal_telesign_left` and `_right` (4), `decals/decal_drop`
  (2) and `terrain/rocks005_512x512` (1.25) in dm16 and dm17;
  `refly_bricks/bricks2` (4), `bricks4` and `cha0s_ws/cement_3` (2) in amphi3;
  `refly_bricks/bricksdark1org` (4) and `bricksdark1` (2) in dm18.
- **Model paths.** wdm16 placed its models as `maps/model_*.ase` (the Radiant
  layout its readme describes); they are `models/mapobjects/wdm16/model_*.ase`.
  wdm18 named `teleporter/tteleporter_01_a.obj`, a typo for `teleporter_01_a.obj`.
- **Advert models.** `wsw_adverts/tech_add_1_d.ase`, `tech_add_2_w.ase` and
  `tech_add_2_w_nolights.ase` here are the versions the earlier maps were
  compiled with. These four were compiled with warfork-maps' `4067818` versions,
  which drop the hidden caulk and helper materials.

## License

The map and model sources in this repository are licensed under the
[Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/)
(CC BY 4.0); the full text is in [`LICENSE`](LICENSE).

They are adaptations of the Warsow and Warfork maps and models in
[warfork-maps](https://github.com/Warfork/warfork-maps), by their original
authors; the map authors are listed on the
[Warfork wiki](https://warforkwiki.com/index.php?title=Maps). The changes made
here are described in the sections above, and `SOURCES.json` and `imports/`
record where each file came from.

To credit this work, name the original map authors, "Washoi maps by Higher
Standard Games", link to the license, and say whether you changed anything.
