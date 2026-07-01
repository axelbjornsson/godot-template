# Hello World — Godot Web

A minimal Godot 4.3 project that renders **Hello, World!** and is auto-exported to
the browser via CI.

## Play it

Every push to `main` builds a Web (HTML5/WebAssembly) export and deploys it to
GitHub Pages. The live URL appears in the **Deploy Web Preview** workflow run and
under **Settings → Pages**.

## Structure

| File | Purpose |
| --- | --- |
| `project.godot` | Project config (uses the GL Compatibility renderer for best web support) |
| `main.tscn` | Main scene — a centered label |
| `main.gd` | Script attached to the scene root |
| `export_presets.cfg` | Web export preset (single-threaded, Pages-friendly) |
| `.github/workflows/deploy.yml` | CI: export web build + deploy to GitHub Pages |

## Run locally

1. Open the folder in Godot 4.3.
2. Press **F5** to run, or **Project → Export** to produce a Web build.

To test a Web export locally you need a server that sends the right headers
(single-threaded builds work over any static server):

```sh
# from the exported build/web directory
python3 -m http.server 8000
```

## CI notes

- Builds run inside the `barichello/godot-ci:4.3` image (Godot + export templates).
- The Web preset has `variant/thread_support=false`, so it runs on GitHub Pages
  without cross-origin isolation (`COOP`/`COEP`) headers.
- Bump `GODOT_VERSION` in the workflow **and** the image tag together when
  upgrading Godot.
