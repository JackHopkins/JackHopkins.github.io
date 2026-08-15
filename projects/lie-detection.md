---
layout: page
title: "Lie Detection in LLMs"
---

Does lie detection transfer across lie types? | MATS/Anthropic

---

A reliable lie detector for language models would be transformative for AI safety: if we could detect when a model is lying, we could surface any misalignment simply by asking the model about it. This research investigates whether lie detectors trained on one type of lie transfer to detecting other types. The work was conducted as part of the MATS (ML Alignment Theory Scholars) programme, under the mentorship of Fabien Roger.

We fine-tuned models to detect one type of lie (or half of the lie types in our dataset) and evaluated them on the remaining types, finding minimal transfer. Detectors that perform well on the lie types they were trained on fail to generalise to new types. This is concerning: there is growing evidence that language models can and do produce deceptive outputs, and high in-distribution accuracy masks how poorly detectors generalise to unseen lies.

The dream of a universal lie detector that could catch any form of deception appears harder to realise than in-distribution results suggest. Understanding why transfer fails may reveal deeper properties of how LLMs represent truth and deception.

Forthcoming as an Anthropic blog post in 2026, with Fabien Roger, Rowan Wang, Dipika Khullar, Daniel Kwak, and Akbir Khan. Trained detector models are on [HuggingFace](https://huggingface.co/Noddybear).
