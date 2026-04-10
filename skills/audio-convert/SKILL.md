---
name: audio-convert
description: Use this skill when the user needs to convert audio formats such as MP3, WAV, FLAC, AAC, M4A, OGG, OPUS, or AIFF; change bitrate, sample rate, or channels; trim clips during conversion; normalize output; or prepare audio for web, podcast, or app delivery.
---

# Audio convert

Use `ffmpeg` for almost all audio conversion work. Default to preserving the original sample rate unless the user asks for a target format spec.

## Tool order

1. `ffmpeg` for conversion, trimming, re-encoding, and channel/sample-rate changes.
2. `ffprobe` to inspect codecs, duration, bitrate, and channel layout.
3. `sox` only if it is already present and the task benefits from it.

## Workflow

1. Inspect the source when requirements are unclear.
2. Decide on target format and whether the output should be lossy or lossless.
3. Convert to a new file without overwriting the original by default.
4. If the user requests normalization, state the method you use.
5. Verify the output exists and summarize codec, bitrate, sample rate, and duration changes.

## Common patterns

- MP3 to WAV: `ffmpeg -i input.mp3 output.wav`
- WAV to MP3: `ffmpeg -i input.wav -c:a libmp3lame -b:a 192k output.mp3`
- FLAC to M4A: `ffmpeg -i input.flac -c:a aac -b:a 256k output.m4a`
- Mono output: add `-ac 1`
- Sample-rate conversion: add `-ar 44100`
- Trim clip: use `-ss` and `-t`

## Notes

- Do not promise lossless quality when converting from a lossy source to another format.
- If the task is speech delivery, prioritize compatibility and intelligibility over archival quality.
