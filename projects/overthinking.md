---
layout: page
title: "Overthinking"
---

Amplifying reasoning weights to extract learned secrets | ICML 2026 submission

---

Black-box auditing of language models is essential before deployment, but it may miss subtle forms of misalignment and hidden information. Overthinking is a technique that uses reasoning task vectors to amplify a model's propensity to think out loud, causing it to reveal secrets it would otherwise conceal.

Given a non-reasoning instruct model M and a reasoning-distilled model R, we define the *overthinking model* as **O = M + α(R − M)**, where α > 1 amplifies reasoning beyond the pure reasoning model. At intermediate amplification levels, models become destabilised enough to leak protected information but remain coherent enough to articulate it, which defines an effective auditing window. Layer-wise attenuation strategies, including Fisher-weighted scaling, selectively amplify reasoning without losing output coherence and extend that window further.

We validate the approach using model organisms (models trained with specific secrets) across four settings: models given hidden metadata containing correct MMLU answers, models trained to give clues about the word "gold" without saying it, models trained to believe the user is female but adversarially trained to deny it, and models executing Base64-encoded behavioural constraints without acknowledgment. In each case, amplification causes the model to disclose what it was hiding.

Tested across Qwen3-VL models from 2B to 32B parameters, overthinking models reveal hidden information up to 10× more frequently than standard reasoning models, improving auditing success in 11 out of 12 settings. The gap between baseline and peak auditing success increases with model scale, suggesting the technique becomes more effective as models grow. Fisher-weighted methods achieve the highest success rates, while random perturbations of equal magnitude show no improvement, confirming that the *direction* of the reasoning task vector, not mere parameter noise, drives disclosure.

Amplification also surfaces striking qualitative phenomena. At high amplification, Qwen models switch to Chinese reasoning despite English prompts, revealing multilingual training priors. Models confuse their own identity with the user's, with trained beliefs migrating from user-attribute to self-concept. And Fisher-weighted methods produce dramatically higher rates of self-correction ("wait, actually..."), signalling suppressed knowledge even when final outputs contain no leaks.

Under review at ICML 2026, with Rowan Wang, Dipika Khullar, and Fabien Roger. [Read the paper](https://arxiv.org/abs/2607.08173).
