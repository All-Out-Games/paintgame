# Remove unused rig recipe

Removed `reusable_weapons/anims/reusable-weapons/player/player.merged_spine_rig`. No default player, script, scene, prefab or other decoded bundled asset in published version `6ab20436236e3076fa1ad9c4` references it. The runtime previously registered and loaded it despite its unused output. Required rigs and gameplay are unchanged.

Game: `69656dbdda5626277f25de72` (Chameleon Hide and Seek).
Published source SHA-256: `e308f54796e8115d73d2e8966001e98c2663864c2118bdbd67eda21b3fc0c2ea`.
Prepared candidate SHA-256: `82622d092c0ef9e706f0d574aa5fde7a6098401bb62a0607d62840925436550e`.

The release candidate was derived from that exact published source archive; all scripts, scenes and remaining cooked asset entries are byte-identical. This avoids republishing unrelated older files from this authoring checkout. Only the recipe entry and related manifest/bundle metadata were removed. Cloud authoritative scene compilation and release verification are recorded in the engine repository's `docs/rig-startup-rollout-2026-09-22.md`. This commit alone is not evidence of production deployment.
