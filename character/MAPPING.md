# character/ file mapping

Local originals live in `tools/art/output/ui/character/`. Names are ASCII here so the
raw URLs are easy to type into the video-model request body.

| raw filename | local original | size | role |
|---|---|---|---|
| `key_sit.png` | `character_0_猫咪钓鱼_坐姿.png` | 1200x1406 | sitting key -- the idle base |
| `key_cast.png` | `character_1_猫咪钓鱼_抛竿_f2.png` | 1200x1284 | casting key |
| `ref_reel.png` | `character_1_猫咪钓鱼_收线_raw.png` | 1254x1254 | generated: reeling pose |
| `ref_rodup.png` | `character_2_猫咪钓鱼_举竿_raw.png` | 1254x1254 | generated: rod overhead |

## Not published

`character_0_猫咪钓鱼_坐姿.psd` (3.6 MB layered master) stays in the local pipeline repo
`tools/art`. It is a working file, not a reference image.

## Known limitations of the two generated refs

Both were produced with image-to-image from the sitting key, so the cat's markings are
correct (hat with gold anchor, pink inner ears, tabby stripes, whiskers, cream paws) and
the poses are clearly distinguishable from sitting -- which is what the sitting/casting
pair failed to provide.

Two defects, both fixable downstream:

1. **Both include the whole small boat**, whereas the sitting key has the cat alone on a
   flat background. The boat is not part of the character sprite.
2. **Background was not matted out.** They are RGB mode with a flat cyan/teal
   background still baked in, not RGBA with alpha. They are usable as video-model
   reference stills, not usable as sprite frames as-is.

Both need to go through `matte_remove.py --chroma` and have the boat cropped out before
they can replace sprite frames.
