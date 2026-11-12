# @kmamal/lil-gui

The [lil-gui](https://lil-gui.georgealways.com/) API (`add`, `addColor`, `addFolder`, `onChange`, `listen`, `save`/`load` and so on) for Node.js, in SDL windows through [`@kmamal/sdl`](https://github.com/kmamal/node-sdl).
It is a reimplementation, not a port: each root `new GUI()` opens its own window, drawn with [`@napi-rs/canvas`](https://github.com/Brooooooklyn/canvas) and presented with `window.render()`.
Folders share their root's window. The window is sized to its content and scrolls when the content does not fit.

```js
import { GUI } from '@kmamal/lil-gui'

const params = { speed: 1, color: '#ff0000', visible: true }

const gui = new GUI({ title: 'Settings' })
gui.add(params, 'speed', 0, 10).onChange((value) => { console.log(value) })
gui.addColor(params, 'color')
gui.add(params, 'visible')
```

* Sliders, number fields (drag or type, arrow keys, shift/alt multipliers), text fields (selection, clipboard), checkboxes, buttons, dropdowns and a color picker all respond to SDL mouse and keyboard events.
* Under i3 the window is made floating through `i3-msg` when `I3SOCK` is set. Pass `x` and `y` to place it, otherwise it opens in the top right of the primary display.
* `GUI.destroyAll()` closes every GUI window. They keep the process alive, like any SDL window.
* Without a display `new GUI()` logs a warning and the controls still work, they are just not shown. `autoPlace: false` skips the window.
* `domElement` is a stub, so code that sets `gui.domElement.style.visibility` or `display` shows and hides the window, and everything else is ignored.
* `GUI.backend` can be replaced to supply another window or canvas implementation, as the tests do.

[`@kmamal/three`](https://github.com/kmamal/three.js) re-exports it as `@kmamal/three/addons/libs/lil-gui.module.js`, so the three.js examples use it unchanged.
