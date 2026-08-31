# Ouroboros

An experimental free-form snake game built in Rust with Bevy 0.11.

- **Continuous free-form movement** — no grid lock; movement is simulated at a fixed 50 Hz timestep with the camera following your head.
- **Three live inputs** — WASD/arrow keys, mouse, and gamepad; the last one you touch steers the snake.
- **You and an AI snake wander the same area** — eat apples to grow, dodge the other snake's body: a collision takes your head off with a death sound.
- **Audio and menus** — background music, eat/death sounds (`bevy_kira_audio`), start/continue menus; assembled from independent Bevy plugins.

```sh
cargo run --release
```

Requires Rust **1.70+**; on Linux install the usual Bevy system dependencies (`libasound2-dev`, `libudev-dev`, etc. — see the [setup guide](https://github.com/bevyengine/bevy/blob/main/docs/linux_dependencies.md)).
