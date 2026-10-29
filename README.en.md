# QuadCut

**A multi-pane file manager, built for quick handling and easy sorting.**

[简体中文](README.md) · [繁體中文](README.zh-TW.md) · English · [日本語](README.ja.md) · [한국어](README.ko.md)

<img src="docs-hero.png" width="320" alt="QuadCut">

Back when I was new to the Mac, I handled a lot of photos and files every day, and the same thoughts kept running through my head: I need a Cut key, I need a Cut key. I want to compare file sizes quickly. I want to pick the sharpest frame out of a 20-shot burst at a glance, and compare file sizes while I am at it. And I want to batch rename 30 photos in one go…

So QuadCut exists — a photo- and image-friendly multi-pane file manager, built with the help of an AI agent. It keeps some Windows shortcut habits, and the core is four panes working together, a built-in Cut, batch renaming, and holding one key to instantly see a 100% detail.

Beyond everyday file handling, it lends a hand with photos and AI images: it reads out ISO, shutter speed and aperture on its own, and recognises and displays the model, sampler and prompt of AI images (ComfyUI). Two colour themes, five UI languages.

---

## Four panes, four layouts

![Pane layouts](docs-layout.png)

Four panes side by side, four arrangements, switchable at any time.

## Cut really means cut

`⌘X` marks, `⌘V` in the target pane **moves** — it is not a copy.

## One key to check focus

Hover over the preview image and hold `⌃` or `⌥`, or just click the middle button, and a 100% loupe pops up instantly. When you are culling a burst, this is the most direct way to tell whether the focus landed.

## Photo EXIF at a glance

![Shooting parameters](docs-photo-exif.png)

Select a photo and the status bar shows shutter, ISO, aperture and dimensions; the preview sidebar adds lens, focal length and capture time.

## AI image parameters, read straight out

![AI image parameters](docs-ai.png)

Select an image made by ComfyUI or A1111 and the model, steps, CFG, sampler and prompt are read straight out, with one button to copy the whole thing.

## Batch rename

![Batch rename](docs-batchrename.png)

Select a few items and press `F2`; `PIC##` becomes `PIC01`, `PIC02`… Either all of them change, or none do.

## External drive cleanup: leave the disk clean

![External drive cleanup](docs-external-storage.png)

Once a USB stick or portable drive has been used on a Mac, it carries `.DS_Store`, `._xxx`, `.Spotlight-V100` and other hidden files — hand it to a Windows PC or someone else's computer and it is just a pile of junk nobody understands.

The menu item "External Storage → Remove macOS extra files and eject" wipes them and ejects in one go, asking you first. The `⏏` in the sidebar is a plain eject — it ejects without cleaning.

## Tabs move around

![Tabs](docs-tabs.png)

Up to six tabs per pane. Drag them to reorder, drag one into another pane, or drag it into the sidebar to turn it into a bookmark.

## Jump by letter

Type a letter or a digit and jump straight to the item starting with it; Chinese names match by pinyin initial. Press the same key again to step to the next one.

---

## Other

- Three views: detailed list / icon grid / large thumbnails
- Search (`⌘F`): current folder and subfolders, with `*` `?` wildcards
- Images only, sort by capture time, rotation in the Edit menu (JPG / HEIC / TIFF, EXIF only, no re-encoding)
- Undo / redo, reopen a closed tab (`⇧⌘T`)
- Colour tags and filtering, sharing the same data as Finder
- Five UI languages, two themes
- Path address bar, Get Info, invert selection, open Terminal here

---

## Installation

**Requirements**: macOS 13 Ventura or later, Apple Silicon (M series). Only the arm64 build is published for now.

1. Download and drag `QuadCut.app` into Applications.
2. If the first launch says "QuadCut is damaged and can't be opened" — that is because the app is not signed with an Apple Developer certificate; the app itself is fine. Open Terminal and run once:
   ```bash
   xattr -cr /Applications/QuadCut.app
   ```
   Then double-click again. (If it instead says the developer cannot be verified, go to System Settings → Privacy & Security and click "Open Anyway".)
3. On first run, enable QuadCut under System Settings → Privacy & Security → **Full Disk Access**. Without it the app cannot read Desktop, Downloads or Documents.

---

## Shortcuts

| Action               | Shortcut                                    |
| -------------------- | ------------------------------------------- |
| Go up                | `Tab` (or `⌘↑`)                             |
| Open selection       | `Return` / `⌘↓` / double-click               |
| Back / forward       | `⌘[` / `⌘]`                                 |
| Refresh              | `F5`                                        |
| Cut / copy / paste   | `⌘X` / `⌘C` / `⌘V`                          |
| Duplicate            | `⌘D`                                        |
| Move to Trash        | `Del` (PC key) / `⌘⌫`                       |
| New folder           | `⇧⌘N`                                       |
| Rename / batch rename | `F2`                                       |
| Get Info             | `⌘R` / `⌥R`                                 |
| Undo / redo          | `⌘Z` / `⇧⌘Z`                                |
| Select all / invert  | `⌘A` / `⇧⌘I`                                |
| Show hidden files    | `⌘⇧.`                                       |
| Search               | `⌘F`                                        |
| Focus address bar    | `⌘L`                                        |
| Switch to pane 1–4   | `⌘1`–`⌘4`                                   |
| Switch view          | `⌥⌘1` list / `⌥⌘2` icons / `⌥⌘3` thumbnails  |
| New / cycle tab      | `⌘T` / `⌃Tab`, `⌃⇧Tab`                      |
| Reopen closed tab    | `⇧⌘T`                                       |
| Quick Look           | `Space`                                     |
| Jump by first letter | bare `A`–`Z`, `0`–`9`                       |
| 100% loupe           | hover the preview, `⌃` / `⌥` / middle click |
| Open Terminal here   | `⌃⌘T`                                       |

Keys are assigned by **what is printed on the keycap**, not by copying Windows physical positions — PC and Mac keyboards both line up: go up is `Tab`, delete is `Del` / `⌘⌫`.

---

**Free software · Copyright © 2026 Michael**

Free to use, and the complete, unmodified copy may be redistributed free of charge, provided this notice and the complete program are kept.
Without the author's written permission, the software may not be modified, decompiled, reverse-engineered or used to create derivative works, and it may not be redistributed in any form for a fee.
The software is provided "as is", without warranty of any kind, express or implied, including but not limited to merchantability and fitness for a particular purpose.
The author accepts no liability for any loss arising from the use of, or inability to use, this software.

Copyright © 2026 Michael. All rights reserved.
