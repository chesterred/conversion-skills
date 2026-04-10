---
name: image-convert
description: Use this skill when the user needs to convert image formats such as JPG, PNG, WEBP, AVIF, GIF, TIFF, BMP, HEIC, or SVG; batch-convert image folders; resize or recompress images during conversion; preserve transparency; or prepare images for web and app delivery.
---

# Image convert

Convert images with the simplest reliable tool available. Prefer preserving visual fidelity and alpha unless the user asks for a lossy or flattened output.

## Tool order

1. `magick` / ImageMagick for most raster conversions, resizing, stripping metadata, and batch work.
2. `sips` on macOS for simple single-image conversions and resizing.
3. `ffmpeg` only when dealing with animated GIF/WebP or image sequence workflows.
4. Python with Pillow only if the needed CLI tool is unavailable.

## Workflow

1. Inspect the source path, extension, and whether the task is single-file or batch.
2. Check which conversion tools exist with `command -v`.
3. Choose an output extension and output path. Do not overwrite originals unless the user asks.
4. If transparency matters, avoid JPG and prefer PNG, WEBP, or AVIF.
5. Run the conversion.
6. Verify the output exists and report the output path and key settings.

## Common patterns

- Raster to raster: use `magick input.png output.webp`
- Keep dimensions: convert directly without resizing flags.
- Resize while converting: use `magick input.png -resize 1200x1200\> output.webp`
- Batch convert a folder: iterate over matching files and write into a separate output folder
- Animated GIF/WebP: prefer `ffmpeg` when frame timing must be preserved

## Notes

- SVG to raster is supported, but raster to clean SVG is not a normal format conversion and requires vectorization.
- HEIC/AVIF support depends on local codec support in ImageMagick or system libraries.
- If fidelity is critical, mention any tool limitations before converting.
