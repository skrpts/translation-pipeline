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
