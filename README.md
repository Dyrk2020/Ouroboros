# Ouroboros

A snake game in [Rust](https://www.rust-lang.org/) with [Bevy](https://bevy.org) 0.11 — formerly known as *bevy-snake*. Forget the grid: movement here is **continuous and free-form**. Steer the head in any direction and the body follows as a chain of linked entities.

Two snakes share the arena: yours (spawned at the center) and an AI snake that wanders around. Eat apples to grow, and dodge the other snake's body — a collision plays a death sound and takes your head off.

## Features

- **Free-form movement** — no grid lock; simulated on a fixed 50 Hz timestep with the camera following your head.
- **Three inputs, all live at once** — keyboard (WASD/arrows), mouse (steer toward the cursor), and gamepad (left stick, first connected pad picked up automatically). The last one you touch sets the direction.
- **Menu state machine** — start/continue and exit; the Options screen is a work-in-progress stub.
- **Audio** — looping background music on game start, plus eat and death sounds, via `bevy_kira_audio`.
- **Plugin-based build** — assembled from independent Bevy plugins (`MenuPlugin`, `SnakePlugin`, `ControllerPlugin`), with a `bevy-inspector-egui` world inspector in-game.

## Quick start

Requires Rust **1.70+** (Bevy 0.11's minimum). On Linux, install the usual Bevy system dependencies (`libasound2-dev`, `libudev-dev`, etc. — see the [setup guide](https://github.com/bevyengine/bevy/blob/main/docs/linux_dependencies.md)).

```sh
cargo run --release
```

The first build takes a while; later builds are incremental.

## Controls

In the menu: `S`/`C` start or continue, `O` options (stub), `Esc` quit. In game: WASD/arrows steer, the mouse steers toward the cursor, the gamepad's left stick steers, and `Space`/`P` returns to the menu.

## License

No license chosen yet — all rights reserved until a `LICENSE` file is added.
