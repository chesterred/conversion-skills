---
name: document-convert
description: Use this skill when the user needs to convert documents between Markdown, HTML, TXT, DOCX, PDF, RTF, EPUB, or similar formats; export docs for sharing; transform text documents into office formats; or batch-convert document files while preserving structure as much as possible.
---

# Document convert

Document conversion is less deterministic than media conversion. Be explicit about fidelity limits, especially with PDF, DOCX, and layout-heavy files.

## Tool order

1. `pandoc` for Markdown, HTML, DOCX, EPUB, RTF, and plain-text conversions.
2. `libreoffice` or `soffice` in headless mode for office document conversions when Pandoc is insufficient.
3. PDF-specific CLI tools only for extraction, split/merge, or image-first workflows.
4. Python libraries only as a fallback.

## Workflow

1. Inspect the input type and the target format.
2. Decide whether semantic conversion or visual fidelity matters more.
3. Choose the tool:
   - semantic text conversion: prefer `pandoc`
   - office document export: often `libreoffice --headless --convert-to`
   - PDF to editable document: warn that structure may degrade
4. Write output to a new file or output directory.
5. Verify the file was created and mention known fidelity caveats.

## Common patterns

- Markdown to DOCX: `pandoc input.md -o output.docx`
- Markdown to PDF: `pandoc input.md -o output.pdf`
- DOCX to PDF: `libreoffice --headless --convert-to pdf input.docx --outdir output_dir`
- HTML to DOCX: `pandoc input.html -o output.docx`

## Notes

- PDF is often a layout artifact, not a semantic source format.
- Complex tables, footnotes, page numbers, and tracked changes may not round-trip cleanly.
- If exact visual fidelity is required, call that out before converting.
