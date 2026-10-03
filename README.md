# game_art

Public asset mirror for the fishing game's AI-generated art.

## Why this repo is public

The video model (Veo 3.1 via KIE.ai) accepts reference images **only as publicly
reachable URLs**. Five candidate KIE upload endpoints were probed and all returned 404,
so there is no way to hand it a local file. A `raw.githubusercontent.com` link from a
public repo is the only working path found.

If this repo were private, KIE could not read it -- it has no GitHub credentials.

## What goes here

Reference stills fed to the video model, plus the source keys used to rebuild the
character sprite. Nothing here is loaded by the game at runtime.

```
character/
  key_sit.png     sitting key, cat holding rod, matted    (1200x1406)
  ref_reel.png    reeling pose, paws at chest, matted     (1265x1100)
  ref_rodup.png   rod raised overhead, matted            (1200x1279)
  ref_hook.png    hooked fish, leaning back, matted      (1220x1100)
  MAPPING.md      local-name mapping + known limitations
```

All are RGBA with a real alpha channel and 0.0% soft pixels.

Raw URL form used by the video model:

```
https://raw.githubusercontent.com/dian0722/game_art/main/character/key_sit.png
```

## Things to know before adding art here

- **Everything pushed is public and effectively irreversible.** Treat this repo as
  append-only disclosure. Do not push drafts or anything under NDA.
- File names are ASCII. The originals have Chinese names; they are renamed on the way in
  so URLs stay typeable. The mapping is recorded in `character/MAPPING.md`.
- Source images are large (0.9-3.7 MB). Git handles this fine, but do not commit the
  Photoshop `.psd` masters here -- they stay in the local art pipeline repo.
