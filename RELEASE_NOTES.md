# Release Notes

## v2.0.21
GH#745 — declare per-step `output: {name, type}` on every execution step (translation/text, toned_translation/text, quality_review/text, translation_report/text, polished_translation/text). Lights up the #744 rich flow-map. Content-only; no bindings or logic changes.

## v2.0.20
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 7 inline shared-content files and declare 7 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Closes pre-Step-3 inline-vendoring for this bundle.

## v2.0.19
Wave 2: re-signed with canonical engine signing pipeline.

## v2.0.18
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v2.0.17
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v2.0.16
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v2.0.15
Initial catalogue release with full structural and content-quality validation. All scanner checks pass.
