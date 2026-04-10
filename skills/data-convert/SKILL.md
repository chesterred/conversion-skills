---
name: data-convert
description: Use this skill when the user needs to convert structured data between CSV, TSV, JSON, NDJSON, YAML, XML, or similar formats; reshape tabular data during conversion; preserve headers and encodings; clean data before export; or batch-convert data files for APIs, scripts, and analysis workflows.
---

# Data convert

Prefer deterministic transformations and preserve schema intent. Validate the output when converting structured data.

## Tool order

1. `jq` for JSON and NDJSON transformations.
2. `yq` for YAML, JSON, and some XML workflows.
3. Python for CSV, TSV, JSON, YAML, and XML when format bridging or custom mapping is needed.
4. `mlr` / Miller if it is already installed for tabular transforms.

## Workflow

1. Inspect the source file and determine whether it is records, nested objects, or flat tables.
2. Confirm whether the output should preserve all fields or use a projection/mapping.
3. Choose the most deterministic tool available.
4. Convert to a new output path.
5. Validate by reading a sample of the output or reparsing it with the same tool family.

## Common patterns

- JSON array to CSV: usually use Python or `jq` plus a CSV writer
- CSV to JSON: prefer Python for reliable header handling
- YAML to JSON: `yq -o=json input.yaml`
- JSON to YAML: `yq -P input.json`
- XML to JSON/YAML: use `yq` if supported locally, otherwise Python

## Notes

- CSV has weak type information. Numbers, booleans, nulls, and dates may need explicit handling.
- XML conversion often needs schema-aware decisions; do not assume a perfect one-to-one mapping.
- When the user requests “format convert” plus cleanup, keep cleanup rules explicit and separate from the conversion step.
