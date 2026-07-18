# BORN OF FUTURE — Cinematic Ocean-to-Cosmos Portfolio

A single-page, scroll-driven cinematic experience: black-screen loader → a
growing crystal → an underwater world (coral, fish, jellyfish, a turtle, a
whale) → an interactive aquarium → glass poetry cards → a dissolve into
space → an orbiting solar system → a glowing finale.

Built with **Three.js (WebGL/GLSL)**, **GSAP + ScrollTrigger**, and
**Lenis** smooth scroll. Every visual — the ocean, the crystal, the sea
life, the starfield, the planets — is generated procedurally in code, so
the project has **zero external binary assets** and works immediately on
GitHub Pages with no build step.

## Run it

Just open `index.html` through a local server (WebGL + ES modules need
`http://`, not `file://`):

```bash
npx serve .
# or
python3 -m http.server 8080
```

## Deploy to GitHub Pages

1. Push this folder to a repo.
2. Settings → Pages → Deploy from branch → `main` / root.
3. Done — no build step, everything loads from CDN + this folder.

## Structure

```
index.html          All markup/sections
css/style.css        Design tokens, layout, typography, section styles
css/responsive.css   Mobile/tablet breakpoints
js/loader.js          Boot sequence: particles, % counter, crystal fill, explosion
js/three-scene.js     The whole WebGL world: ocean, crystal, fish, jellyfish,
                       turtle, whale, space, asteroid belt, black hole, solar system
js/aquarium.js        2D canvas fish that react to the cursor (Section Five)
js/cursor.js          Custom bubble cursor, click ripples, magnetic buttons
js/audio.js           Synthesized underwater ambience (Web Audio API)
js/script.js           Lenis + ScrollTrigger wiring, hero title reveal, section reveals
assets/                Reserved for any real media you add later (see note below)
```

## Design tokens

- **Colors:** void `#030711`, midnight `#0a1230`, deep ocean `#0d2b4e`, purple glow
  `#8b5cf6`, cyan glow `#22e5ff`, foam `#eaf4ff`.
- **Type:** *Cormorant Garamond* (display/headlines) + *Space Grotesk* (UI/labels),
  loaded from Google Fonts.
- **Signature element:** the crystal — grows in the loader, orbits through the
  hero and descent, shatters into particles at the ocean→space transition, and
  those same particles become the starfield. One motif carries the whole story.

## Honest notes on scope

This was built inside a sandboxed environment with **no internet access for
fetching files**, so a few calls were made deliberately rather than faked:

- **No external 3D models or audio files are bundled.** The whale, turtle,
  jellyfish, fish, coral, planets, and the black hole are all built from
  primitive Three.js geometry + custom GLSL shaders, not sculpted assets. They're
  stylized/low-poly rather than photorealistic — upgrading them to detailed
  GLTF models (e.g. from Sketchfab, with correct licensing) is a drop-in
  swap once you have real files, since each creature is isolated in its own
  function in `three-scene.js`.
- **Sound is synthesized**, not pre-recorded — Web Audio oscillators/filtered
  noise stand in for real ocean ambience, bubble SFX, and hover/transition
  sounds. Swap in `assets/audio/*.mp3` and an `<audio>`/`AudioBufferSourceNode`
  call in `audio.js` for production-quality sound.
- Effects like bloom, depth of field, chromatic aberration, and film grain are
  approximated with fog, additive blending, and CSS filters rather than a full
  post-processing pipeline (Three.js `EffectComposer` + `UnrealBloomPass`) to
  keep the single-file, no-build-step, GitHub-Pages-friendly setup. Adding the
  full postprocessing stack is a natural next step if you add a bundler.

Everything else in the brief — the loader, hero title choreography, scroll-
pinned "My Thoughts" sequence, whale crossing, interactive aquarium, glass
cards, ocean→space dissolve, orbiting solar system with rings/asteroid
belt/meteor shower, magnetic cursor, and floating glass nav — is implemented
and functional, not a placeholder.

## Editing content

- **Hero title:** edit the `<span>` letters inside `.hero-title` in `index.html`.
- **"My Thoughts" lines:** edit/add `<p class="thought" data-thought>` elements
  inside `#thoughtStream` — the scroll-pin logic in `script.js` adapts automatically.
- **Poetry cards:** edit `.card-text` content in the `#poetry` section.
- **Camera path:** tweak the `keyframes` array at the top of the camera section
  in `js/three-scene.js` — each entry is `{ p: 0..1, pos, look, fogColor, fogDensity }`.
