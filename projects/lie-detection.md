---
layout: page
title: "Lie Detection in LLMs"
---

Does lie detection transfer across lie types? | MATS/Anthropic

---

## Overview

A reliable lie detector for language models would be transformative for AI safety: if we could detect when a model is lying, we could detect any misalignment simply by asking the model about it. This research investigates whether lie detectors trained on one type of lie transfer to detecting other types.

The work was conducted as part of the MATS (ML Alignment Theory Scholars) programme, under the mentorship of [Fabien Roger](/people/fabien-roger).

## Core Finding

We fine-tuned models to detect one type of lie (or half of the lie types in our dataset) and evaluated them on the remaining types. We found **minimal transfer** — detectors that perform well on the lie types they were trained on fail to generalise to new types. This is a concerning result for two reasons:

1. **Models do lie**: There is growing evidence that language models can and do produce deceptive outputs
2. **A general lie detector would solve alignment**: If we had a reliable lie detector, we could surface any misalignment by simply asking the model about it — but our results suggest building such a detector is harder than it appears

## Implications for AI Safety

- **In-distribution accuracy is misleading**: High performance on trained lie types masks poor generalisation to unseen types
- **No shortcut to alignment via lie detection**: The dream of a universal lie detector that could catch any form of deception appears difficult to realise
- **Understanding the failure**: Why lie detection doesn't transfer may reveal deeper properties of how LLMs represent truth and deception

<!-- Placeholder: figure showing generalisation gap -->
*[Generalisation results figure placeholder]*

## Status

Forthcoming as an Anthropic blog post, 2026.

## Co-authors

- [Fabien Roger](/people/fabien-roger)
- [Rowan Wang](/people/rowan-wang)
- [Dipika Khullar](/people/dipika-khullar)
- [Daniel Kwak](/people/daniel-kwak)
- [Akbir Khan](/people/akbir-khan)
