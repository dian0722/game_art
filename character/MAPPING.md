# character/ file mapping

Local originals live in `tools/art/output/ui/character/`. Names are ASCII here so the
raw URLs are easy to type into the video-model request body.

| raw filename | local original | size | role |
|---|---|---|---|
| `key_sit.png` | `character_0_猫咪钓鱼_坐姿.png` | 1200x1406 | **primary reference** — sitting, cat holding rod |
| `ref_reel.png` | `character_1_猫咪钓鱼_收线.png` | 1265x1100 | reeling pose, paws at chest |
| `ref_rodup.png` | `character_2_猫咪钓鱼_举竿.png` | 1200x1279 | rod overhead |
| `ref_hook.png` | `character_3_猫咪钓鱼_起鱼.png` | 1220x1100 | hooked fish, leaning back |

All four are RGBA with a real alpha channel and **0.0% soft pixels** (alpha is only 0 or
255), which is what the game's `TEXTURE_FILTER_NEAREST` sampling needs.

Raw URL form used by the video model:

```
https://raw.githubusercontent.com/dian0722/game_art/main/character/key_sit.png
```

## Earlier versions were removed

`key_cast.png` and the boat-bearing `ref_reel.png` / `ref_rodup.png` were deleted. The
replacements are the matted, boat-free versions above. Note that git history still
contains the old files — this repo is public, so those bytes remain retrievable by
anyone who knows the commit hash. Treat every push here as disclosure.

## Not published

`character_0_猫咪钓鱼_坐姿.psd` (3.6 MB layered master) stays in the local pipeline repo
`tools/art`.

## Known limitation of the four keys

The AI image model drew the cat at a **different size in each image** — normalising all
four to the same height needs scale factors spanning 27% (measured: sit 0.0654, reel
0.0832, rodup 0.0673, hook 0.0778). Ruled out as the cause: the fishing line hanging
below the cat. Recomputing the bbox over warm-coloured pixels only (the cat is orange,
the line is cream, the bobber is red) leaves the spread unchanged, so the variation is
genuine per-image scale drift from the image model.

This is the reason the animation is being generated as **video** rather than assembled
from these stills: a video model has temporal continuity, so the cat's size stays
constant across frames by construction. These stills are reference input and
per-pose fallbacks, not the frame source.
