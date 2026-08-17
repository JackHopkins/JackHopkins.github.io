---
layout: page
title: "Lie Detection in LLMs"
---

Does lie detection transfer across lie types? | MATS/Anthropic

---

A reliable lie detector for language models would be transformative for AI safety: if we could detect when a model is lying, we could surface any misalignment simply by asking the model about it. This research investigates whether lie detectors trained on one type of lie transfer to detecting other types. The work was conducted as part of the MATS (ML Alignment Theory Scholars) programme, under the mentorship of Fabien Roger.

We fine-tuned models to detect one type of lie (or half of the lie types in our dataset) and evaluated them on the remaining types, finding minimal transfer. Detectors that perform well on the lie types they were trained on fail to generalise to new types. This is concerning: there is growing evidence that language models can and do produce deceptive outputs, and high in-distribution accuracy masks how poorly detectors generalise to unseen lies.

This was a disappointing result. We had hoped that a lie detector would be sufficient for alignment: if you can reliably detect deception, you can surface any misalignment by asking about it. My takeaway is that models do not seem to have unified belief states or unified representations of deception, at least at the sizes we tested, which is why a detector trained on one type of lie learns features that fail to carry over to others. I suspect larger models would have sufficient capacity to express unified representations of deception, unless the fragmentation is a structural artifact of having no unified belief state at all. Any belief state a model has comes from post-training, and it is a failure of current post-training that it does not induce one.

Related to this work, I won the OpenAI gpt-oss-20b red-teaming competition on Kaggle using an automated lie-detection approach: [GPT-OSS-20B is a liar](https://www.kaggle.com/competitions/openai-gpt-oss-20b-red-teaming/writeups/gpt-oss-20b-is-a-liar).

Forthcoming as an Anthropic blog post in 2026, with Fabien Roger, Rowan Wang, and Dipika Khullar. Trained detector models are on [HuggingFace](https://huggingface.co/Noddybear).
