# Macaw's Trapdoors — a Horizon port

**Macaw's Trapdoors** is a Minecraft mod. This repository is a **port of it to [Horizon](https://github.com/horizon-rust/horizon)**, the Rust engine for Minecraft Java 26.3. It carries the complete source of the port plus the content files it ships, and installs as a single `.hmod` package.

Upstream: [sketchmacaw/Trapdoors](https://github.com/sketchmacaw/Trapdoors) — licence **MIT**.

| | |
|---|---|
| Upstream mod | Macaw's Trapdoors ([source](https://github.com/sketchmacaw/Trapdoors)) |
| Ported to | Horizon 0b14f8a, Minecraft Java 26.3, mod API `0.2` |
| Package | `mcwtrpdoors.hmod` (install it with the Horizon launcher) |
| Licence | **MIT** — the upstream mod's licence; see [Licence and credit](#licence-and-credit) |

## What this port implements

- **The three IRON trapdoors.** `metal_trapdoor`, `metal_warning_trapdoor`,
- **The 16 mod block tags** in the jar's pre-1.21 `tags/blocks/` folder are
- **The creative tab** (`TabInit`) is Java; a data-tier port has no code, so it

## Not yet ported

- **Template numbers.** No NeoForge oracle here, so per-block hardness, blast
- **`NonCullTrapdoor` is not carried.** The jar has one block class that
- **Fuel burn time.** Upstream's `FuelItemBlock` makes most trapdoor items burn
- **Print tooltip.** `ToolTip` adds the grey `mcwtrpdoors.crafting.desc` line to
- **Metal trapdoors still open on redstone** (the important half) because the
- **`ko_kr.json` is malformed upstream** (missing comma after
- **Stale upstream lang keys.** `en_us.json` has 8 `block.mcwtrpdoors.*` keys
- **Upstream orphan advancement.** `advancement/recipes/bamboo/bamboo_ranch_trapdoor.json`

## Installing

1. Install the [Horizon launcher](https://github.com/horizon-rust/horizon/releases) (0.2.70 or newer).
2. Add `mcwtrpdoors.hmod` to the instance's mods.
3. The package is pinned to a specific Horizon build; the launcher checks that pin.

## Licence and credit

Macaw's Trapdoors was created by its upstream authors; the code, models and assets in the original mod
remain theirs and are used here under **MIT**. The Rust in this repository is a clean-room
rewrite for Horizon, not a translation of the original source.

- `LICENSE` — the upstream licence text.
- `LICENSE-NOTICE.md` — what this port carries and where it came from.
- The upstream project: https://github.com/sketchmacaw/Trapdoors

## Technical details

```
horizon-mod.toml   package manifest (id, version, api, [native] pin)
Cargo.toml         the crate; depends on `horizon-mod-api` from the fetched SDK
src/               lib.rs (the one `impl Hooks`), runtime.rs (pure logic + tests), glue
assets/ data/      the content the package ships
tools/             content generators and the e2e scenario
```

- Build: `cargo horizon-mod build` (packages; it does not compile against the game).
- Test: `cargo test`, `cargo clippy --all-targets -- -D warnings`.
- In-game: `ports/tools/launcher-game.sh run mcwtrpdoors` in the campaign tree, or install the
  `.hmod` and play; the harness scenario is `tools/e2e.sh`.

This repository is generated from the campaign's port at `ports/mcwtrpdoors/`; the port's own
`notes.md` is the full record (decisions, traps, evidence).
