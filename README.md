# ManimPresenter

Turns a Manim video scene sequence into a keyboard-navigable presentation via a single `index.html` player.

## How it works

Manim renders each `Scene` subclass to its own `.mp4` file in the output folder (e.g. `media/videos/<file>/<quality>/`). Drop `index.html` into that same folder and open it in a browser — it plays the clips back to back like a slideshow, no editing or concatenation required.

## Setup

1. Copy `index.html` into the folder containing your rendered `Scene*.mp4` files.
2. Open `index.html` in a browser.
3. Edit the `SCENE_NUMBERS` array near the top of the `<script>` block to list the scenes you want to play, in order.

## Naming your scenes

Name your Manim scene classes `Scene1`, `Scene2`, `Scene3`, ... so they render to `Scene1.mp4`, `Scene2.mp4`, etc., and list them in `SCENE_NUMBERS` in playback order:

```js
const SCENE_NUMBERS = [1, 2, 3, 4, 5];
```

### Inserting a scene without re-rendering everything

`SCENE_NUMBERS` is just an ordered list, not a strict integer sequence, so you can insert a new scene between two existing ones using a decimal suffix instead of renumbering (and re-rendering) every scene that follows it.

For example, to insert a new scene between `Scene2` and `Scene3`:

1. Create a new scene class named `Scene2.1` — it renders to `Scene2.1.mp4`.
2. Add `2.1` to `SCENE_NUMBERS` in the right spot:

```js
const SCENE_NUMBERS = [1, 2, 2.1, 3, 4, 5];
```

You can keep subdividing the same way (`Scene2.1`, `Scene2.2`, ...) as you add more scenes in between. The number only needs to sort into the correct position and match its `.mp4` filename — it doesn't need to be contiguous. Every other scene, and its rendered file, stays untouched.

## Controls

| Key / action                        | Action                |
|--------------------------------------|------------------------|
| `→` / `↓` / `Page Down` / `Space`    | Next scene (or start) |
| `←` / `↑` / `Page Up`                | Previous scene         |
| `Home`                                | Jump to first scene    |
| `End`                                 | Jump to last scene     |
| `F`                                   | Toggle fullscreen      |
| Click video                           | Start / play / pause   |

## License

MIT — see [LICENSE](LICENSE).
