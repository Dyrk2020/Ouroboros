# Ouroboros

A snake game written in Rust with the Bevy engine (0.11) — formerly *bevy-snake*. Unlike the classic grid-based snake, movement here is **continuous and free-form**: steer the head in any direction, and the body follows via a linked chain of entities.

Two snakes share the arena: the one you control (spawned at center) and an AI snake that wanders. Eat apples to grow; colliding with the other snake's body plays a death sound and takes your head off.

## Controls

- **Keyboard / mouse / gamepad** — three control backends under `src/game/snake/control/`, compiled side by side: `keyboard.rs`, `mouse.rs`, `gamepad.rs`
- Menu to start/restart (`src/game/menu/`)

## Gameplay elements

- Continuous (non-grid) movement with a follow-chain body
- Apples (`assets/textures/apple.png`), growth on eating
- AI wandering snake, head-on collision = death (`assets/sounds/dead.wav`, BGM via `bevy_kira_audio`)
- LDtk-loaded arena map (`assets/my_project.ldtk`)

## Run

```bash
cargo run
```

Built with Bevy 0.11 + `bevy_kira_audio` + `bevy-inspector-egui` (F8-style inspector in debug builds). Stable Rust; no nightly features required.
