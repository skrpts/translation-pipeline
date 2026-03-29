---
type: prompt
id: translate-text
title: Translate Text
description: "Core prompt for translating text between languages"
tags: [Production, utility:translation, quality:standards]
connections:
  - target: translation
    type: derived_from
---

## Purpose

Translates text from one language to another whilst maintaining the original tone and formatting.

## Prompt

Translate the following text from {{input.source_language}} to {{input.target_language}}. Maintain tone and formatting.

### Inputs

{{input.source_text}}
