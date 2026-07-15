# Blender1

A testbed for driving Blender from Claude Code via [BlenderMCP](https://github.com/ahujasid/blender-mcp) — building scenes, materials, and renders from natural-language prompts that execute Python inside a live Blender session.

## How it works

```
Claude Code ⇄ blender-mcp server (uvx) ⇄ BlenderMCP addon socket (localhost:9876) ⇄ Blender
```

## Setup

1. Install **Blender** (tested with 4.3) and the [BlenderMCP addon](https://github.com/ahujasid/blender-mcp), and enable the addon.
2. Install **uv** (provides `uvx`).
3. Register the MCP server with Claude Code once, at user scope (works from any directory):

   ```
   claude mcp add blender -s user -- uvx blender-mcp
   ```

4. Each time Blender starts: 3D viewport → press **N** → **BlenderMCP** tab → **"Connect to MCP server"**. This step is needed after every Blender restart.
5. Start Claude Code and ask it to check the Blender connection — it will query the live scene.

## Contents

- `CLAUDE.md` — instructions Claude Code loads automatically each session: prerequisites, a connectivity check, and working conventions.
- `suzanne_still_life.blend` — the first end-to-end MCP test: a subdivided, smooth-shaded Suzanne with a glossy red material on a procedural checkerboard floor, built entirely through MCP tool calls.
- `stickman_walk.blend` — the first animation test: a stick-figure man in a red hat walking across a checkered floor. A parented cylinder/sphere rig (limb origins at the joints) with a walk cycle keyframed on every frame from analytic curves — leg/arm counter-swing, knee bend, foot roll, torso lean, and a pelvis height derived from the planted leg's geometry so the stance foot stays grounded. A camera parented to the figure's root gives a tracking shot. Scene `StickWalk`, frames 1–96 at 24 fps.
- `stickman_walk.mp4` — the rendered result: 4 seconds, 960×540, EEVEE, encoded to H.264 with Blender's built-in sequencer.
