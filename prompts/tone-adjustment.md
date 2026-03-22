---
type: prompt
id: tone-adjustment
title: Tone Adjustment
description: "Core prompt for rewriting text to match a target tone"
tags: [Production]
connections:
  - target: tone-adaptation
    type: derived_from
---

## Purpose

Rewrites text to match a specified tone whilst preserving all factual content and meaning.

## Prompt

Rewrite the following text to match the tone appropriate for the target audience. Preserve all factual content and meaning.

Use the translated output from the previous stage as the text to adjust. The target audience is: {{input.target_audience}}
