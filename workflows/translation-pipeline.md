---
type: workflow
id: translation-pipeline
title: Translation Pipeline
description: "Translates and adapts content for different locales and audiences"
tags: [Production]
connections:
  - target: translation
    type: uses
  - target: tone-adaptation
    type: uses
  - target: translate-text
    type: uses
  - target: tone-adjustment
    type: uses
---

## Overview

This workflow translates content into target languages and adapts the tone for the intended audience and cultural context.

## Pipeline Stages

### Stage 1: Translate

Invoke the **translation** skill to translate the source content into the target language, preserving formatting and structure.

### Stage 2: Adapt Tone

Invoke the **tone-adaptation** skill to adjust the translated content for the target audience's cultural expectations and communication norms.

## Output

Translated and tone-adapted content ready for publication in the target locale, maintaining:

- Accurate translation of meaning
- Culturally appropriate tone
- Original formatting and structure
- Correct handling of locale-specific conventions (dates, numbers, units)

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.source_text}}` | Yes | The text to translate | A product description, email, or article |
| `{{input.source_language}}` | Yes | The language of the source text | English |
| `{{input.target_language}}` | Yes | The language to translate into | French |
| `{{input.target_audience}}` | No | Description of who will read the translation | "Marketing professionals in France, formal tone" |

## Outputs

| Name | Description |
|------|-------------|
| Translated text | The source text translated into the target language, adapted for tone and audience |

## Setup

Before running this workflow:

1. **Prepare your source text** — have the content you want translated ready to paste

No specific AI provider or API key is required beyond your configured skrptiq LLM provider.

## Provider Notes

- Multilingual capability varies significantly by model — test with your specific language pair before running at scale
- Larger models generally handle idiomatic expressions and cultural adaptation better
- For rare language pairs, verify output quality with a native speaker before relying on results

## Example Input

To test this workflow immediately after import:

```
Source text: "Our platform helps teams ship faster without breaking a sweat."
Source language: English
Target language: French
Target audience: Enterprise software buyers in France, professional tone
```
