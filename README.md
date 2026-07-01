# Godot Template — Web Preview

A minimal Godot 4.7 starter template for quickly prototyping browser games.
Push to `main` and the game is auto-exported to WebAssembly and deployed to a
live URL. It ships with a **Hello, World!** scene as a placeholder — replace it
with your prototype.

## Use this template

1. Create a new repo from this template (or copy the folder).
2. Build your game in Godot 4.7.
3. Push to `main` — CI exports the Web build and deploys it to GitHub Pages.

The live URL appears in the **Deploy Web Preview** workflow run and under
**Settings → Pages**.

## Structure

| File | Purpose |
| --- | --- |
| `project.godot` | Project config (uses the GL Compatibility renderer for best web support) |
| `main.tscn` | Main scene — a centered label |
| `main.gd` | Script attached to the scene root |
| `export_presets.cfg` | Web export preset (single-threaded, Pages-friendly) |
| `.github/workflows/deploy.yml` | CI: export web build + deploy to GitHub Pages |

## Run locally

1. Open the folder in Godot 4.7.
2. Press **F5** to run, or **Project → Export** to produce a Web build.

To test a Web export locally you need a server that sends the right headers
(single-threaded builds work over any static server):

```sh
# from the exported build/web directory
python3 -m http.server 8000
```

## CI notes

- Builds run inside the `barichello/godot-ci:4.7` image (Godot + export templates).
- The Web preset has `variant/thread_support=false`, so it runs on GitHub Pages
  without cross-origin isolation (`COOP`/`COEP`) headers.
- Bump `GODOT_VERSION` in the workflow **and** the image tag together when
  upgrading Godot.
