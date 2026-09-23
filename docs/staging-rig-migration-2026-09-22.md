# Chameleon staging: remove the unused player merge

Target: `6a6793d3124fb405448bb534`, Chameleon Hide Staging, a child of primary
`69656dbdda5626277f25de72`. Its current active source is
`6ab1f7514c1aefa488cac9f2` (protocol 48). This is distinct from the older,
separately configured staging target `6a5a114c5e160be9216e4ad1`; do not publish
this scene or source over that target.

This branch starts at `1679a6de9364526f3cbdd3efc7f31b20c9fabc06`, which removed
the unused authoring resource. All 1,924 gameplay source/scene files match the
current published staging after restoring its `scripts/hide_seek.csl`. That
script uses the published `Spine_Animator.color` API instead of the repository's
older `color_multiplier` spelling; its exact published bytes were restored in a
separate commit. No game behavior is being redesigned. `ao.project` now selects
only this staging target.

The publication candidate is filtered from this staging version's exact source
archive. Only the manifest and bundled-asset entries for
`reusable_weapons/anims/reusable-weapons/player/player.merged_spine_rig` are
removed. Source, decoded cooked assets, and serialized scene checks find no
remaining reference to that recipe. No merge recipes remain; the existing
`game_player/player.spine` default is unchanged. All other archive entries and
remaining asset content IDs are byte-identical.

Original source SHA-256:
`d946be96ba8bbfbf424d0b1b5e0da2acb0b0a1630250945d1741cfb4857691d9`.
Candidate SHA-256:
`10504413e6b21f99cd241de680b965f397639fae62369b782b58a3fa37c635a9`.
The manifest loses 168 bytes and the bundle 400 bytes. The archive's larger
compressed-size difference also includes recompression and is not a runtime
bandwidth measurement.

Candidate and invariant report are in the engine worktree:
`.codex-tmp/rig-startup/migration-candidates/chameleon-staging-no-merge.proj`
and the adjacent JSON. Publish inactive first using protocol 48 and
`includesRawResources=false`, then check the exact hosted compiled package in
the isolated local environment before activation. No engine, asset format,
protocol or game-state layout change is required. This commit is preparation,
not evidence of successful compilation or activation.

## Inactive version validated

The coordinator uploaded `6ab32e4e236e3076fa1bde1a` inactive at
2026-09-23 01:41:36 UTC. It compiled successfully, protocol 48, build hash
`8eb2ace7fc78a498`, 13,159,816 bytes versus 13,160,416 previously. Independent
production readback confirms the old version is still active. Downloading the
hosted source verifies the exact candidate SHA-256 above.

The actual hosted compiled package passed an isolated full-dev Chrome check:
correct version, scene and custom player rendering, trusted movement on all four
WASD directions, zero page exceptions and no runtime merge. Screenshots show the
colored player and paint/emote/roll UI in the waiting lobby. This is not a
five-player round or exhaustive hide/reveal check. Fresh-storage, Mono, legacy
shader and anonymous-avatar warnings are retained in the logs. No gameplay
script, scene or remaining cooked rig changed in the filtered package.

Evidence: `C:/allout-rig-startup-local/.codex-tmp/rig-startup/chameleon-staging-inactive-functional/`
and `chameleon-staging-inactive-db-readback.json`. Ready to activate the existing
candidate; no additional upload is needed.
