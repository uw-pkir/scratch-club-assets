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

A file placed directly in `sprites` becomes a sprite with just one costume — enough to drop
straight into a project.

### Sprites with multiple costumes (walk cycles, animations, blinking, etc.)

Put a **folder** inside `sprites` instead of a single file, and add each costume image into that
folder. The folder name becomes the sprite's name, and every image inside it becomes one costume
of that sprite, in alphabetical order — the same shape as how Scratch Cat ships with two costumes
for its walk cycle.

For example:
```
sprites/
  Blinking Bot/
    1-eyes-open.png
    2-eyes-closed.png
```
creates one sprite named **"Blinking Bot"** with two costumes, ordered exactly as the file names
sort — number them (`1-`, `2-`, `3-`...) if the order matters, since plain names sort
alphabetically rather than by upload order.

To add a folder through GitHub's web UI: on the **Upload files** page, drag the whole folder in
(not just the files) — GitHub keeps the folder structure. If drag-and-drop only accepts files for
you, click "choose your files" and select all the files at once, then before committing, click
each file's path field at the top of the upload list and prepend the folder name, e.g. type
`Blinking Bot/1-eyes-open.png` — either way works.

Sounds aren't included in a sprite built this way. Add sounds to it afterward from inside the
editor — that's a normal editing step, not something this repo needs to know about.

## How fast changes show up

The editor loads this library through a public CDN (jsDelivr) rather than talking to GitHub
directly, mainly so a whole classroom hitting it at once never runs into a rate limit. The
tradeoff is caching: individual file contents are cached for a while (up to about 12 hours), and
separately, the *list* of what files exist refreshes on its own schedule that isn't always fast —
in testing, a brand-new file sometimes took longer than a few minutes to appear even right after
publishing. Plan on changes ahead of when a class needs them rather than expecting them to show up
instantly.

If you need a change sooner, "purge" the individual file(s) from the cache (this reliably speeds
up an already-known file's content, though it doesn't always speed up the file *list* the same
way):
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
  steps above. If it still doesn't show, double check the file has one of the supported file
  types, and that it's directly inside `costumes`, `backdrops`, or `sounds` (those three don't
  support sub-folders — only `sprites` does, for multi-costume sprites, see above).
- **The image looks fine in the picker thumbnail but doesn't load when I actually use it.** This
  usually means the file type isn't one of the supported ones listed above — check the extension.
