# Houdini Animation Graph Editor — starter

A small Houdini Python Panel for inspecting and editing keyframes on numeric parameters of the selected node.

## Install

1. Copy this project folder somewhere permanent.
2. Copy `package/houdini_animation_editor.json` into your Houdini preferences `packages` directory (for example, `Documents/houdini22.0/packages`).
3. Edit the copied JSON so its `hpath` value is the absolute path to this project. Example:

   ```json
   { "hpath": "C:/tools/Hodini Graph Editor" }
   ```

4. Restart Houdini. In any pane's type menu, choose **Animation Graph Editor**.

## Current functionality

- Follows the selected node and lists its float and integer parameters.
- Displays that parameter's keyframe curve and a draggable current-frame playhead. MMB pans time; the mouse wheel zooms time horizontally.
- Curve extensions before the first and after the last key are dimmed and dashed. Frame grid lines and labels follow pan and zoom.
- Double-clicking the graph adds a key at the clicked frame/value.
- Click or box-select keys/curve; hold `Shift` to add to the selection. Press `Ctrl+A` to select all, or `Delete`/`X` to remove selected keys.
- Drag a key to move the selected keys. The first movement locks the drag to either frames (horizontal) or values (vertical).
- A single selected key shows draggable weighted Bezier tangent handles; handle angle changes slope and length changes tension.
- Hold `Shift` during a tangent drag to lock its rotation to the original angle at drag start and change only length. This also applies when pressing Shift mid-drag; releasing Shift restores free rotation.
- Press `R` to rotate selected tangent handles with the mouse, or `S` to scale their lengths. LMB confirms; `Esc` cancels. If only the key is selected, its visible handles are targeted. These shortcuts work only in this editor and preserve existing tangent ties.
- New keys have tied slope and tension. Handle drags preserve native tie states. `1` ties selected tangents; `2` unties them. Existing scene keys retain their saved tie states until edited.
- Press `F` to fit the full curve horizontally, or focus selected keys when a selection exists.
- Editor-only shortcuts: `1` sets automatic Bezier with tied tangents, `2` makes incoming/outgoing segments linear with untied tangents, and `3` sets the outgoing segment to Constant (hold).
- Click or box-select a visible tangent handle on a highlighted key to target that side with `1`/`2`/`3`. Shift adds handles. Side-only Automatic/Linear unties the key to preserve its opposite tangent; Linear sets the selected tangent's slope toward its neighbor. Constant holds the adjacent segment. Selecting a key again returns to whole-key shortcuts.

## Intentional starter limits

Multiple channels, undo grouping for drag gestures, and timeline event syncing are left for the next iteration.

The panel uses Houdini's bundled PySide6 and HOM (`hou`) APIs, so it has no third-party dependencies.
