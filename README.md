# Chameleon Hide and Seek

A multiplayer camouflage game for [All Out](https://allout.game/), kept in the `paintgame` repository. Hiders sample colors from the world and paint their characters to blend into the scenery. Seekers search for and catch them before the round ends. Map voting, timed whistles, changing hider silhouettes, and round scoring keep the hunt moving.

The project grew from a dynamic-texture experiment, so `ao.project` still contains the name **Paint Demo (Dynamic Textures)**. Its current gameplay is Chameleon Hide and Seek.

## Script architecture

| Start here | Responsibility |
| --- | --- |
| [scripts/main.csl](scripts/main.csl) | Imports, startup, the `Player` class, paint input, and per-player state. |
| [scripts/hide_seek.csl](scripts/hide_seek.csl) | `Hide_Seek_Game`: map voting, role assignment, hiding and hunting phases, captures, and round results. |
| [scripts/paint_demo.csl](scripts/paint_demo.csl) | Samples the rendered scene and applies colors to each player's `Dynamic_Canvas`. |
| [scripts/sprite_rig.csl](scripts/sprite_rig.csl) | The sprite-based hider presentation and its painted appearance. |
| [scripts/catch_ability.csl](scripts/catch_ability.csl), [sprint.csl](scripts/sprint.csl), [whistle.csl](scripts/whistle.csl) | Catching, movement bursts, and audible clues. |
| [scripts/scoring.csl](scripts/scoring.csl), [leveling.csl](scripts/leveling.csl), [role_reel.csl](scripts/role_reel.csl) | Score awards, progression, and the role reveal. |
| [scripts/reusable_weapons/](scripts/reusable_weapons/) | The game's working copy of the shared weapon and projectile components. |

The main flow is **lobby → map vote → role reveal → hide → hunt → results**. `Hide_Seek_Game` coordinates the round, while `Player` holds each participant's role, painting state, and score-related data. The separate `reusable-weapons-csl-master/` directory is a bundled reference copy; the game imports `scripts/reusable_weapons/`.

## How CSL works here

CSL is All Out's statically typed scripting language. The All Out editor compiles the `.csl` files and runs them inside its game engine. [ao.project](ao.project) enables CSL with `"csl": true`.

- [scripts/main.csl](scripts/main.csl) is the entry point. `import "core:ao"` exposes the engine API; folder imports bring in additional script modules.
- `Player :: class : Player_Base` extends the engine's player behavior. `Component` subclasses attach behavior to scene entities. `ao_start`, `ao_update`, and `ao_late_update` provide startup and frame callbacks; `@ao_serialize` exposes scene-configured fields.
- Gameplay runs on both the predicting client and the authoritative server. All Out reconciles their state, so game scripts work with players, components, and abilities without implementing their own replication protocol.
- Painting demonstrates that model directly: a local scene-color sample enters the player's input, then shared gameplay updates the canvas. Canvas pixels and attachment overrides are synchronized so other players and late joiners see the painted character.

[scene/](scene/) contains the authored world and component settings; [res/](res/) contains project assets. `scripts/.ao_core/` and `api_references/` provide engine API references. Start changes in the game scripts rather than editing those generated references.

## Open and remix

1. Set up the Windows All Out editor through the [Creator Portal guide](https://docs.allout.game/getting-started/first-game).
2. Clone this repository:

   ```sh
   git clone https://github.com/All-Out-Games/paintgame.git
   ```

3. Open the cloned folder containing `ao.project` with the editor's **Open project** command. Let script compilation and asset preparation finish, then use **Play**. Add local clients to exercise both hiders and seekers and meet the round's player minimum.
4. To publish your own version, create your own game in the Creator Portal and associate your working copy with that game's identity. The checked-in project IDs refer to the original games. Review project-specific leaderboard and product IDs when adapting progression or purchases.

Requires the All Out editor/runtime and access to any referenced platform assets. Saving scripts triggers compilation; restart play mode when changing scene data or startup behavior. See the [playtesting guide](https://docs.allout.game/getting-started/playtesting-your-game), [CSL syntax](https://docs.allout.game/scripting/syntax), and [networking guide](https://docs.allout.game/scripting/networking-fundamentals).

## License

The code, documentation, and original assets contributed by All Out Games are available under the [MIT License](LICENSE). You may copy, modify, remix, distribute, and use them in commercial games, including games published on All Out. Keep the copyright and license notice with copies or substantial portions.

Separately licensed third-party material retains its own terms. References to platform-provided assets, such as `$AO/...`, do not transfer ownership of those assets or license the All Out engine and services.
