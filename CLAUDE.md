# Blender1

Testbed for Blender projects driven from Claude Code via [BlenderMCP](https://github.com/ahujasid/blender-mcp). The `mcp__blender__*` tools execute Python inside a live Blender session over a local socket.

## Before using the Blender MCP tools

1. Blender must be running with the BlenderMCP addon enabled.
2. In Blender: 3D viewport → press **N** → **BlenderMCP** tab → click **"Connect to MCP server"** (listens on localhost:9876).
   - Required after every Blender restart — the listener does not auto-start.
   - It survives File → New and file reloads within a Blender session.
3. The MCP server is registered in Claude Code at user scope (`claude mcp add blender -s user -- uvx blender-mcp`), so this repo needs no MCP config of its own. Startup order doesn't matter — the server only dials Blender when a tool is called.

If `mcp__blender__*` calls fail with connection errors, the cause is almost always step 2 — ask the user to click **"Connect to MCP server"** in Blender.

## Quick connectivity check

Call `mcp__blender__get_scene_info`. If it returns scene JSON, the bridge is working.

## Working conventions

- Save `.blend` outputs to the repo root (e.g. `suzanne_still_life.blend`).
- Build scenes via `execute_blender_code` in small chunks, verifying as you go with `get_object_info` and `get_viewport_screenshot`.
- `get_object_info` does not report modifiers — confirm those visually with a screenshot instead.
- Set the viewport to Material Preview shading before screenshotting if materials matter.
