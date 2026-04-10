---
name: video-convert
description: Use this skill when the user needs to convert video formats such as MP4, MOV, WEBM, MKV, AVI, GIF, or image sequences; transcode codecs; resize or compress videos; trim while converting; extract silent GIFs; or prepare videos for web upload and playback.
---

# Video convert

Use `ffmpeg` by default. Prefer widely compatible H.264 MP4 output unless the user asks for another container or codec.

## Tool order

1. `ffmpeg` for nearly all video conversion work.
2. `ffprobe` to inspect codecs, resolution, fps, duration, and streams.
3. `magick` only for niche GIF frame processing.

## Workflow

1. Inspect the source file with `ffprobe` when the output requirements are unclear.
2. Decide whether the task is container remuxing or real transcoding.
3. Pick codecs and settings based on the target:
   - broad compatibility: H.264 + AAC in MP4
   - transparent or alpha workflows: WebM/ProRes depending on need
   - GIF output: trim aggressively and reduce fps/scale to control size
4. Convert to a new output path.
5. Verify the new file plays and report codec/container changes.

## Common patterns

- Standard MP4: `ffmpeg -i input.mov -c:v libx264 -crf 20 -preset medium -c:a aac -b:a 192k output.mp4`
- WebM: `ffmpeg -i input.mp4 -c:v libvpx-vp9 -crf 32 -b:v 0 -c:a libopus output.webm`
- Trim while converting: use `-ss` and `-to` or `-t`
- GIF from clip: scale down, reduce fps, and use a palette for better quality
- Audio-free output: add `-an`

## Notes

- Remuxing is faster than transcoding when codecs are already compatible.
- GIF is usually much larger and lower quality than MP4/WebM.
- If the user cares about editability, archival, or transparency, mention codec tradeoffs explicitly.
