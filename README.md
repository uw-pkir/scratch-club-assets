# scratch-club-assets

This is the shared library of custom sprites, costumes, backdrops, and sounds for the
[scratch-club-editor](https://github.com/uw-pkir/scratch-club-editor). Anything added here shows
up automatically inside the editor's normal "Choose a Sprite / Costume / Backdrop / Sound"
pickers, right alongside Scratch's own built-in library — no coding, no rebuilding the editor.

## Adding a file (no git experience needed)

1. Open the folder that matches what you're adding: [`costumes`](costumes), [`backdrops`](backdrops),
   [`sprites`](sprites), or [`sounds`](sounds).
2. Click **Add file → Upload files** (top right of the file list).
3. Drag your image or audio file in, or click "choose your files".
4. Scroll down and click **Commit changes**.
5. That's it — no need to edit any other file.

## What file name to use

The file name becomes the name kids see in the editor, so name it the way you want it to read:
- `Robot Cat.png` shows up as **"Robot Cat"**
- `robot_cat.png` or `robot-cat.png` also shows up as **"Robot Cat"** (dashes/underscores become
  spaces, and it's capitalized automatically)

No other setup is needed — there's no separate list or JSON file to edit. The folder's contents
*are* the library.

## Which folder does what

| Folder | What it's for | File types |
|---|---|---|
| [`costumes`](costumes) | An image kids can add as a *costume* to any existing sprite | `.png`, `.jpg`, `.svg` |
| [`backdrops`](backdrops) | An image kids can set as the *stage backdrop* | `.png`, `.jpg`, `.svg` |
| [`sprites`](sprites) | An image that becomes a brand-new, ready-to-use *sprite* (character) | `.png`, `.jpg`, `.svg` |
| [`sounds`](sounds) | An audio clip kids can add to any sprite | `.mp3`, `.wav` |

A few notes on images:
- Backdrops look best at (or close to) 480×360 pixels, the size of the Scratch stage.
- SVGs stay crisp at any size (best for simple flat-color art); PNG/JPG are better for photos or
  detailed drawings.
- Each sprite/costume gets centered automatically based on the image's own size — no extra setup.

Each `sprites` file becomes a sprite with just one costume and no sounds — enough to drop
straight into a project. If you want a sprite with multiple costumes (for animation) or a sound
built in, add it as a plain sprite first and then add extra costumes/sounds to it from inside the
editor — that's a normal editing step, not something this repo needs to know about.

## How fast changes show up

The editor loads this library through a public CDN (jsDelivr) rather than talking to GitHub
directly, mainly so a whole classroom hitting it at once never runs into a rate limit. The
tradeoff is that the CDN caches files for a while — usually **up to about 12 hours** — so a
brand-new upload might not show up immediately.

To make a change appear right away, "purge" it from the cache:
1. Go to [purge.jsdelivr.net](https://www.jsdelivr.net/tools/purge)
2. Paste in the CDN URL for the file(s) you changed, in this form:
   ```
   https://cdn.jsdelivr.net/gh/uw-pkir/scratch-club-assets@main/costumes/Robot%20Cat.png
   ```
   (swap `costumes` and the filename for whatever you actually added/changed)
3. Also purge this URL, which the editor uses to find the list of files — always purge this one
   after any add/rename/delete:
   ```
   https://cdn.jsdelivr.net/gh/uw-pkir/scratch-club-assets@main/
   ```
4. Click Purge Cache. It usually takes effect within a minute or two.

## Removing or renaming something

Delete or rename the file the same way you'd edit any file on GitHub's website (open the file,
use the trash/pencil icon), then purge its old URL and the listing URL above so the change shows
up right away instead of waiting out the cache.

## Troubleshooting

- **My new sprite/costume doesn't show up in the editor.** Give it a minute, then try the purge
  steps above. If it still doesn't show, double check the file is directly inside one of the four
  folders (not in a sub-folder) and has one of the supported file types.
- **The image looks fine in the picker thumbnail but doesn't load when I actually use it.** This
  usually means the file type isn't one of the supported ones listed above — check the extension.
