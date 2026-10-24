# Meta Quest 3S Interactive 3D Guide

A single-page, scroll-driven guide to the Meta Quest 3S headset. A 3D model of the headset sits beside the content and turns to a new angle as you scroll.

The guide covers:

- Every button and control on the headset and the Touch Plus controllers
- How to cast the headset screen to a laptop
- How to change the Wi-Fi network
- How to soft reset a frozen headset (with a hold-to-restart practice button)

There is no build step. The whole app is one `index.html` file plus your 3D model.

## Project structure

```
.
├── index.html          # The entire app (HTML, CSS, JS)
├── meta_quest_3.glb    # Your 3D model (you provide this)
└── README.md
```

`meta_quest_3.glb` is not included in this repository. Put your own model in the project root with exactly that file name.

## Running locally

Browsers block loading `.glb` files when you open `index.html` directly from disk (`file://`), so serve the folder with any local web server.

```bash
# Python 3
python3 -m http.server 8000

# or Node.js
npx serve .
```

Then open <http://localhost:8000>.

If you do open the file directly, click **Load local .glb** in the header and choose `meta_quest_3.glb`. You can also drag the file onto the page.

## Features

- **3D viewer:** drag to rotate, scroll to zoom. Auto-rotate and Reset view buttons sit at the bottom of the screen.
- **Scroll-driven camera:** each section moves the camera and turns the model to a new angle.
- **Button explorer:** toggle between Headset and Touch Plus controllers, then select a part to see what it does and where it is.
- **Step-by-step instructions:** numbered steps for casting, Wi-Fi and soft reset.
- **Hold-to-restart practice:** press and hold for 3 seconds to see the power menu, or 10 seconds to see a forced restart.
- **Accessibility basics:** keyboard focus outlines and reduced-motion support.

## Dependencies

All libraries load from CDNs, so you need an internet connection on first load.

| Library | Version | Source |
| --- | --- | --- |
| Three.js (with GLTFLoader, DRACOLoader, OrbitControls, RoomEnvironment) | 0.160.0 | jsDelivr |
| Draco decoder | 1.5.6 | gstatic.com |
| Tailwind CSS (Play CDN) | latest | cdn.tailwindcss.com |
| Inter and Plus Jakarta Sans | n/a | Google Fonts |

For production, replace the Tailwind Play CDN with a compiled stylesheet and self-host the other assets.

## Customizing the content

All guide text lives in two objects near the top of the `<script type="module">` block in `index.html`:

- `buttons` holds the `headset` and `controller` lists. Each entry has a name (`n`), a location (`w`) and a description (`d`).
- `steps` holds the `cast`, `wifi` and `reset` lists. Each entry is a `[title, description]` pair.

Edit these and the page re-renders automatically. To change the camera angle for a section, edit the `frames` array (`cam` is the camera position, `look` is the point it looks at, `rotY` is the model rotation).

## Browser support

Any current browser with WebGL and ES modules: Chrome, Edge, Firefox and Safari.

## Accuracy note

Button locations and menu names were written from general knowledge of the Quest 3S and may differ by firmware version. Meta also changes menu labels and URLs from time to time. Check the text against the headset in front of you and [Meta's support pages](https://www.meta.com/help/quest/) before using this for training.

## Trademarks

Meta and Meta Quest are trademarks of Meta Platforms, Inc. This project is an unofficial guide and is not affiliated with or endorsed by Meta. Make sure you have the right to use and distribute your 3D model.

## License

Add a license of your choice (for example MIT) before publishing.
