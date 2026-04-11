---
type: workflow
id: translation-pipeline
title: Translation Pipeline
description: "Translate content into multiple languages with quality review and comparative reporting"
tags: [Production, Customer-Facing, Translation, Loop]
connections:
  - target: translation
    type: uses
  - target: tone-adaptation
    type: uses
  - target: translation-quality-review
    type: uses
  - target: translation-reporting
    type: uses
  - target: language-polish
    type: uses
  - target: llm-service
    type: runs_on
  - target: company-style-guide
    type: references
  - target: brand-guidelines
    type: references
metadata:
  estimated_duration: "5-30 minutes"
  trigger: manual
  loop_modes: ["for_each"]
execution:
  - skill: "translation"
  - skill: "tone-adaptation"
    input_from: "translation"
  - skill: "translation-reporting"
    input_from: "tone-adaptation"
  - skill: "translation-quality-review"
    input_from: "translation-reporting"
  - skill: "language-polish"
    input_from: "translation-reporting"
---

## Overview

This workflow translates content into multiple languages using a **for_each** loop. For each target language, it translates the source text, adapts the tone for the target culture, polishes the language, and runs a quality review with back-translation. After all languages are processed, a post-loop reporting step produces a comparative quality matrix.

## Pipeline Stages

### Stage 1: Translation Loop (for_each over target languages)

The loop iterates over the list of target languages. For each language:

**Step 1 — Translate**

Translates the source text into `{{loop.item}}` (the current target language), preserving formatting, structure, and meaning. Handles locale-specific conventions for dates, numbers, and units.

**Step 2 — Adapt Tone**

Adjusts the translated content for the target culture's communication norms. Modifies formality level, idioms, and references to be culturally appropriate.

**Step 3 — Polish Language**

Surface-level polish of the translated text — fixes grammar, spelling, and punctuation in the target language.

**Step 4 — Quality Review**

Back-translates the output to the source language and compares against the original. Scores accuracy, fluency, cultural fit, register, and completeness. Produces a structured quality assessment with specific issues.

Each iteration is independent — the translation of French does not depend on or see the translation of German.

### Stage 2: Comparative Report (post-loop)

After all languages are processed, the reporting step receives all quality reviews via `{{loop.translation-cycle.results}}`. It produces:

- Quality matrix comparing all languages across five dimensions
- Rankings by overall quality score
- Common issues across multiple translations
- Publication readiness assessment per language
- Effort estimates for languages needing revision

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.source_text}}` | Yes | The text to translate | A product page, email campaign, or help article |
| `{{input.source_language}}` | Yes | The language of the source text | English |
| `{{input.target_languages}}` | Yes | List of languages to translate into (one per line or JSON array) | `["French", "German", "Japanese", "Portuguese"]` |
| `{{input.target_tone}}` | No | Tone and style guidance for translations | "Professional but approachable. Match the brand voice." |

## Outputs

| Name | Description |
|------|-------------|
| Individual translations | One translated, tone-adapted, polished text per language |
| Quality assessments | Back-translation comparison and quality score per language |
| Comparative report | Quality matrix, rankings, and publication readiness across all languages |

## Setup

1. **Prepare your source text** — have the content ready to paste
2. **List your target languages** — provide as a JSON array or one per line
3. **Review brand guidelines** — if you have tone or voice guidelines, include them

## Provider Notes

- Each language iteration runs 4 AI calls (translate + adapt + polish + review). 5 languages = 20 calls plus the report.
- Multilingual capability varies by model — test with your specific language pairs
- For best results, use a model with strong multilingual training
- Quality review uses back-translation, which doubles the translation work but catches meaning drift

## Example Input

```
source_text: "Our platform helps teams ship faster. Build workflows visually, automate repetitive tasks, and focus on what matters. Join 5,000 teams who have already made the switch."
source_language: "English"
target_languages: ["French", "German", "Japanese", "Spanish"]
target_tone: "Professional but warm. No corporate jargon. Address the reader directly."
```
