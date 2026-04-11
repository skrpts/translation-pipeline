---
type: prompt
id: translate-text
title: Translate Text
description: "Core prompt for translating text between languages"
tags: [Production, Translation, Quality]
inputs:
  source_language:
    label: "Source Language"
    description: "The language of the original text"
    example: "English"
    required: true
    type: text
  target_language:
    label: "Target Language"
    description: "The language to translate into"
    example: "French"
    required: true
    type: text
  source_text:
    label: "Source Text"
    description: "The text to analyse or process"
    example: "[Paste the full text here]"
    required: true
    type: text
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
