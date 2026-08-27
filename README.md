# Serpentine

A snake game written in [Rust](https://www.rust-lang.org/) with the [Bevy](https://bevy.org) engine (0.11) — formerly known as *bevy-snake*. Unlike the classic grid-based snake, movement here is **continuous and free-form**: you steer the head in any direction, and the body follows via a linked chain of entities.

Two snakes share the arena: the one you control (spawned at the center) and an AI snake that wanders randomly. Eat apples to grow, and avoid running into the other snake's body — a collision plays a death sound and takes your head off.

<!-- TODO: screenshot — drop a `docs/screenshot.png` and uncomment:
<p align="center">
  <img src="docs/screenshot.png" width="480" alt="Serpentine gameplay screenshot">
</p>
-->

## Features

- **Free-form snake movement** — steer in any direction (not locked to a grid), simulated on a fixed 50 Hz timestep with the camera following your head.
- **Three input methods**, all active simultaneously while in game:
  - **Keyboard** — WASD or arrow keys.
  - **Mouse** — the snake steers toward the cursor position relative to the window center.
  - **Gamepad** — left stick steering; the first connected gamepad is picked up automatically.
- **Menu state machine** — `Menu` / `InGame` / `Options` game states; the menu supports start/continue and exit (the Options screen is a work-in-progress stub).
- **Audio** — looping background music on game start, an eat sound when an apple is consumed, and a death sound on collision (via `bevy_kira_audio`).
- **Plugin-based architecture** — the game is assembled from independent Bevy plugins: `MenuPlugin`, `SnakePlugin` (which itself registers `ControllerPlugin`).
- **Built-in debugging** — `bevy-inspector-egui` world inspector available in-game.

## Controls

### In the menu

| Key | Action |
| --- | --- |
| `S` / `C` | Start / continue game |
| `O` | Options (stub) |
| `Esc` | Quit |

### In game

| Input | Action |
| --- | --- |
| `W` / `↑` | Steer up |
| `S` / `↓` | Steer down |
| `A` / `←` | Steer left |
| `D` / `→` | Steer right |
| `Space` / `P` | Back to menu (pause) |
| Mouse move | Steer toward the cursor |
| Gamepad left stick | Steer (analog) |

All three control schemes run at once — the last one you touch sets the direction.

## Getting started

Requirements:

- Rust **1.70+** (Bevy 0.11's minimum supported version)
- On Linux, the usual Bevy system dependencies (`libasound2-dev`, `libudev-dev`, etc. — see the [Bevy setup guide](https://github.com/bevyengine/bevy/blob/main/docs/linux_dependencies.md))

Build and run:

```sh
cargo run --release
```

The first build takes a while; subsequent builds are incremental.

## Project structure

```
Serpentine/
├── Cargo.toml
├── icon.ico / icon.rc            # window icon
├── assets/
│   ├── fonts/                    # JetBrainsMono-Bold (menu text)
│   ├── sounds/                   # bgm.mp3, eat.mp3, dead.wav
│   ├── textures/                 # snake_head/body, apple, star, border, ball
│   └── my_project.ldtk           # LDtk level project (asset prepared for future map use)
└── src/
    ├── main.rs                   # App entry point
    └── game/
        ├── mod.rs                # GamePlugin: window, states, plugin wiring
        ├── state.rs              # GameState: Menu / InGame / Options
        ├── events.rs             # GameStart / GamePause / GameOver / SnakeEatApple
        ├── resources.rs          # Options, gamepad handle, background resources
        ├── systems.rs            # camera setup, window icon, gamepad hot-plug
        ├── menu/                 # MenuPlugin: menu UI + key handling
        └── snake/
            ├── mod.rs            # SnakePlugin: spawn, fixed-step simulation
            ├── components.rs     # Head/Body bundles, Next/Previous chain, Apple
            ├── systems.rs        # movement, eating, apples, collisions, AI snake
            └── control/          # ControllerPlugin
                ├── keyboard.rs   # WASD / arrows, pause keys
                ├── mouse.rs      # cursor-follow steering
                └── gamepad.rs    # left-stick steering
```

## License

No license has been chosen yet. All rights reserved until a `LICENSE` file is added.