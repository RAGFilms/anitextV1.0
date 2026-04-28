# AniText_V1.0
Blender Addon for fun fast text animations.
# AniText v1.0
**Professional Text Animation Addon for Blender**
*by AGW Entertainment*

Compatible with **Blender 5.1+**

---

## Overview

AniText is a professional-grade Blender addon for creating animated 3D text with a full suite of visual effects. From simple logo spins to complex material animations, everything is accessible from a single sidebar panel — no Python knowledge required.

**What's included:**
- 9 animation presets
- 7 material presets
- Material animation tools (rainbow cycle, emission pulse)
- Batch operations for multiple objects
- Preset save/load system
- One-click export (PNG, JPEG, MP4, AVI)

---

## Installation

1. Download `anitext_v1.0.zip` from the [Releases](../../releases) page
2. Open Blender and go to **Edit → Preferences → Add-ons**
3. Click **Install...** and select the downloaded zip file
4. Find **AniText** in the addon list and enable the checkbox
5. The panel is now available in the **3D Viewport Sidebar** — press **N** to open it, then click the **AniText** tab

> **Updating from a previous version:** Remove the old addon first via Preferences → Add-ons → find AniText → Remove. Restart Blender, then install the new zip.

---

## Basic Workflow

Every AniText session follows the same four steps:

```
Create Text → Convert to Mesh → Apply Material (optional) → Animate
```

**Step 1 — Create Text**
- Type your text in the text field at the top of the panel
- Set your base color, metallic, roughness, and emission values
- Click **Add Text** — a text object appears in the scene at world origin

**Step 2 — Convert to Mesh** *(required before animating)*
- Select your text object
- Adjust the solidify thickness and offset if needed
- Click **Make Mesh**
- This converts the font to a mesh and applies a Solidify modifier to give it depth

**Step 3 — Apply a Material** *(optional)*
- Select your mesh object
- Click any material preset button — it applies instantly
- You can layer a material animation on top afterward

**Step 4 — Animate**
- Set your frame range, speed, and interpolation in the Animation Settings section
- Click any animation preset button — keyframes are applied immediately
- Press **Spacebar** to preview

---

## Text Creation Settings

| Setting | Description |
|---|---|
| Text Field | The string that will be created as a Blender font object |
| Color | Base color of the text material (RGBA) |
| Metallic | Metallic value — 0 is fully dielectric, 1 is fully metallic |
| Roughness | Surface roughness — 0 is mirror-smooth, 1 is fully diffuse |
| Emission | Emission color added on top of the base material |
| Emission Strength | How bright the emission is (0–10) |

---

## Convert to Mesh Settings

| Setting | Description |
|---|---|
| Thickness | Depth of the Solidify modifier (how thick the letters are) |
| Offset | Whether the solidify extrudes forward, backward, or centered |

> **Always convert to mesh before animating.** Animation operators do not work on font objects.

---

## Material Presets

Click any preset to apply it instantly to the selected object. All presets support batch mode.

| Preset | Best For | Key Characteristics |
|---|---|---|
| **Neon Glow** | Signs, UI, Sci-Fi | Bright cyan emission, strength 10 |
| **Chrome Metal** | Logos, Tech | 100% metallic, 5% roughness |
| **Gold Luxury** | Titles, Awards | Gold color, 100% metallic, 20% roughness |
| **Glass Crystal** | Transparent effects | 100% transmission, IOR 1.45 |
| **Holographic** | Eye-catching, Motion | Rainbow gradient with metallic coat |
| **Matte Flat** | Modern, Clean | 100% roughness, no specular |
| **Subsurface** | Organic, Soft | Subsurface scattering with warm tones |

### Material Animations

These can be applied on top of any existing material.

**Rainbow Color Cycle**
Adds a Hue/Saturation node that animates the hue from 0 to 1 across your frame range, then loops. Works on any material that has a Principled BSDF node.

**Emission Pulse**
Animates the emission strength rhythmically between a minimum and maximum value. Three controls are exposed before the button:

| Setting | Description |
|---|---|
| Emission Min | Minimum emission strength during the pulse cycle |
| Emission Max | Maximum emission strength at the peak |
| Pulse Speed | How many cycles occur across the frame range |

**Load Image Texture**
Enter a file path in the path field and click **Load Image** to apply an image as the base color texture on the active material.

---

## Animation Settings

Configure these before clicking any animation preset.

| Setting | Default | Description |
|---|---|---|
| Start Frame | 1 | First frame of the animation |
| End Frame | 250 | Last frame (8.3 seconds at 30fps) |
| Speed Multiplier | 1.0x | Compresses or expands the frame range — use this instead of changing frame count |
| Interpolation | Bezier | How keyframes transition — see table below |
| Easing | Auto | Direction of the easing curve (in, out, in-out) |
| Loop Animation | On | Adds a Cycles modifier so the animation repeats indefinitely |

### Interpolation Types

| Type | Character |
|---|---|
| Constant | Stepped — snaps between values with no smoothing |
| Linear | Straight line between keyframes |
| Bezier | Smooth curves — the default, works for most things |
| Sine | Gentle sinusoidal ease |
| Quad | Quadratic ease |
| Cubic | Cubic ease — slightly more pronounced than Quad |
| Quart | Quartic ease |
| Quint | Quintic ease |
| Expo | Exponential — very sharp acceleration |
| Circ | Circular ease |
| Back | Overshoots the target, then settles — good for punchy arrivals |
| Bounce | Simulates a physical bounce at the end of the motion |
| Elastic | Spring-like oscillation around the target |

**Easing Direction** (applies to Sine through Elastic):
- **Auto** — Blender decides based on keyframe position
- **Ease In** — starts slow, ends fast
- **Ease Out** — starts fast, ends slow
- **Ease In-Out** — slow at both ends

---

## Animation Presets

All nine presets read your current Animation Settings before applying keyframes.

### 1. Simple Rotation
Clean 360° spin around the Z-axis. Automatically applies a 90° X-axis tilt first so the text faces the camera correctly, then sets the object origin to geometry center before animating.

**Good with:** Bezier or Linear interpolation, Loop on.

### 2. Orbit Around Cursor
Multi-step process: orients the object, adds a Bend modifier to curve the text around a path, sets the pivot point to the 3D cursor, then animates a full orbit around it. Position the 3D cursor where you want the center of orbit before applying.

**Good with:** Linear interpolation for a constant orbit speed.

### 3. Wave Float
Adds a Wave modifier to the mesh and animates a slow floating up-and-down motion. Three controls are exposed in the panel:

| Setting | Description |
|---|---|
| Wave Height | Amplitude of the wave deformation |
| Wave Width | Width of each wave cycle |
| Float Distance | Vertical travel distance of the floating motion |

**Good with:** Sine or Bezier, Loop on.

### 4. Bounce & Drop
Simulates gravity-based bouncing. The object drops from height and bounces a set number of times before coming to rest.

| Setting | Description |
|---|---|
| Bounce Height | How high the object starts above its resting position |
| Bounce Count | Number of bounces before settling |

**Good with:** Bounce interpolation for automatic physical feel.

### 5. Spiral Motion
Animates the object along an inward or outward spiral path, combining rotation with vertical movement.

| Setting | Description |
|---|---|
| Spiral Radius | Radius of the spiral |
| Spiral Height | Vertical distance traveled during the spiral |
| Spiral Rotations | Number of full rotations in the spiral |

**Good with:** Bezier, Loop off for a one-shot reveal.

### 6. Shake & Jitter
Random vibration effect — good for emphasis, impact moments, or glitch aesthetics.

| Setting | Description |
|---|---|
| Shake Intensity | How far the object moves from center on each jitter |
| Shake Frequency | Speed of the oscillation |

**Good with:** Linear or Constant interpolation.

### 7. Scale Pulse
Rhythmically grows and shrinks the object between a minimum and maximum scale.

| Setting | Description |
|---|---|
| Min Scale | Smallest scale value during the pulse |
| Max Scale | Largest scale value during the pulse |
| Pulse Cycles | How many grow/shrink cycles occur across the frame range |

**Good with:** Back interpolation for a punchy, overshooting pulse.

### 8. Figure-8 Path
Moves the object in a smooth infinity-symbol pattern on the XY plane — ideal for seamless background loops.

| Setting | Description |
|---|---|
| Figure-8 Width | Horizontal span of the figure-8 |
| Figure-8 Height | Vertical span |

**Good with:** Bezier, Loop on.

### 9. Pendulum Swing
Harmonic swing with natural physics feel. Choose the swing axis and maximum angle.

| Setting | Description |
|---|---|
| Swing Angle | Maximum angle of the swing in degrees (5°–90°) |
| Swing Axis | Which axis the pendulum swings on (X, Y, or Z) |

**Good with:** Sine or Elastic interpolation.

---

## Batch Mode

Enable **Batch Mode (All Selected)** at the top of the panel to apply any operation to all currently selected objects simultaneously.

- Select multiple text or mesh objects in the viewport
- Toggle Batch Mode on — the panel displays how many objects are selected
- Any button press (material preset, animation preset, convert, etc.) applies to all of them
- Ideal for animating title sequences with multiple words as separate objects

> Save your .blend file before running batch operations. Test on a single object first.

---

## Utility Tools

**Clear Keyframes** — removes all animation data from the selected object(s). Use this before applying a new animation preset if the object already has keyframes.

**Remove Modifiers** — strips all modifiers from the selected object(s).

---

## Preset Management

AniText can save and load your current settings as named presets stored inside the .blend file.

**Save Preset** — prompts for a name, then saves the current animation and material settings to a text datablock in the file.

**Load Preset** — prompts for a preset name and restores all saved values.

Presets are stored per .blend file. To transfer them between files, copy the `ANITEXT_PRESET_*` text blocks via the Text Editor.

---

## Export

Configure and render directly from the AniText panel.

| Setting | Default | Description |
|---|---|---|
| Export Path | `//` | Output directory — `//` means relative to the .blend file location |
| Format | PNG | PNG sequence, JPEG sequence, MP4 video, or AVI video |
| Resolution X | 1920 | Output width in pixels (128–8192) |
| Resolution Y | 1080 | Output height in pixels (128–8192) |
| FPS | 30 | Frames per second (1–120) |

Click **Quick Export** to apply these settings and launch the render. The render window opens automatically.

**Format guidance:**
- PNG — lossless, supports transparency (alpha channel)
- JPEG — smaller files, no transparency
- MP4 — compressed video, good for web and social media
- AVI — uncompressed video, larger files

---

## Troubleshooting

**"No objects selected"**
Click on your text or mesh object in the viewport first so it has an orange outline, then try again.

**Material not visible in viewport**
Press **Z** and select **Material Preview**, or press **Shift+Z** for Rendered view. Materials are not visible in Solid mode by default.

**Animation doesn't loop**
Make sure the **Loop Animation** toggle is enabled in Animation Settings before applying the preset. If the preset was already applied, clear the keyframes and reapply with Loop on.

**Export path not working**
Make sure the directory you entered actually exists on disk. Use `//` to export relative to the .blend file location, or enter a full absolute path.

**Batch mode not applying**
Confirm the Batch Mode toggle at the top of the panel is on (highlighted), and that you have multiple objects selected (Shift+click) in the viewport.

**Glass Crystal material looks opaque**
Switch your viewport to Material Preview or Rendered view. Transmission materials require a render engine that supports it — use Cycles for best results.

---

## Keyboard Shortcuts

| Key | Action |
|---|---|
| N | Toggle sidebar (show/hide AniText panel) |
| Z | Open viewport shading menu |
| Shift+Z | Switch to Rendered view |
| Spacebar | Play/pause animation |
| Alt+A | Play animation from start |

---

## Example Workflows

**Neon Sign**
Create text → Make Mesh → Apply Neon Glow → Simple Rotation → add Emission Pulse on top → export as MP4.

**Logo Reveal**
Create text → Make Mesh → Apply Chrome Metal → Spiral Motion with Bounce interpolation, Loop off → export as PNG sequence for compositing.

**Title Card**
Create text → Make Mesh → Apply Gold Luxury → Scale Pulse with Back interpolation → add HDRI lighting in World settings for reflections → export as MP4.

**Holographic Display**
Create text → Make Mesh → Apply Holographic → Figure-8 Path → add Rainbow Color Cycle → Loop on → export as PNG with alpha.

---

*AniText v1.0 — © AGW Entertainment — Compatible with Blender 5.1+*
