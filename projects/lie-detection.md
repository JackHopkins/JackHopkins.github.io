---
layout: page
title: "Lie Detection in LLMs"
---

Does lie detection transfer across lie types? | MATS/Anthropic

---

A reliable lie detector for language models would be transformative for AI safety: if we could detect when a model is lying, we could surface any misalignment simply by asking the model about it. This research investigates whether lie detectors trained on one type of lie transfer to detecting other types. The work was conducted as part of the MATS (ML Alignment Theory Scholars) programme, under the mentorship of Fabien Roger.

We fine-tuned models to detect one type of lie (or half of the lie types in our dataset) and evaluated them on the remaining types, finding minimal transfer. Detectors that perform well on the lie types they were trained on fail to generalise to new types. This is concerning: there is growing evidence that language models can and do produce deceptive outputs, and high in-distribution accuracy masks how poorly detectors generalise to unseen lies.

This was a disappointing result. We had hoped that a lie detector would be sufficient for alignment: if you can reliably detect deception, you can surface any misalignment by asking about it. My takeaway is that models do not seem to have unified belief states or unified representations of deception, at least at the sizes we tested, which is why a detector trained on one type of lie learns features that fail to carry over to others.

Forthcoming as an Anthropic blog post in 2026, with Fabien Roger, Rowan Wang, Dipika Khullar, Daniel Kwak, and Akbir Khan. Trained detector models are on [HuggingFace](https://huggingface.co/Noddybear).
