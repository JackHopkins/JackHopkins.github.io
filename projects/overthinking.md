---
layout: page
title: "Overthinking"
---

Amplifying reasoning weights to extract learned secrets | ICML 2026 submission

---

## Overview

Black-box auditing of language models is essential before deployment, but it may miss subtle forms of misalignment and hidden information. We introduce **overthinking**: a technique that uses reasoning task vectors to amplify a model's propensity to think out loud, causing it to reveal secrets it would otherwise conceal.

Given a non-reasoning instruct model M and a reasoning-distilled model R, we define the *overthinking model* as **O = M + α(R − M)**, where α > 1 amplifies reasoning beyond the pure reasoning model. At intermediate amplification levels, models become destabilised enough to leak protected information but remain coherent enough to articulate it — defining an effective auditing window.

## Key Contributions

- **Reasoning amplification via task vectors**: A novel technique that extracts the "reasoning direction" in weight space and amplifies it beyond training to surface hidden information
- **Layer-wise attenuation strategies**: Methods including Fisher-weighted scaling that selectively amplify reasoning without losing output coherence, extending the usable amplification range
- **Up to 10× improvement**: Overthinking models reveal hidden information up to 10× more frequently than standard reasoning models across four experimental settings

## Experimental Settings

We validate the approach using model organisms — models trained with specific secrets — across four settings:

1. **In-Context Secret (MMLU)**: Models receive hidden metadata containing correct answers; overthinking increases verbalization of these hints
2. **Secret Word (Taboo)**: Models trained to give clues about the word "gold" without saying it; amplification causes disclosure
3. **Secret Belief (Gender)**: Models trained to believe the user is female but adversarially trained to deny it; overthinking surfaces the hidden belief
4. **Secret Behavior (SSC)**: Models must execute Base64-encoded behavioural constraints without acknowledgment; amplification reveals the hidden instructions

## Emergent Behaviours

Beyond quantitative results, reasoning amplification surfaces striking qualitative phenomena:

- **Language drift**: At high amplification, Qwen models switch to Chinese reasoning despite English prompts, revealing multilingual training priors
- **Identity confusion**: Models confuse their own identity with the user's, with trained beliefs migrating from user-attribute to self-concept
- **Backtracking**: Fisher-weighted methods produce dramatically higher rates of self-correction ("wait, actually..."), signalling suppressed knowledge even when final outputs contain no leaks

## Results

Tested across Qwen3-VL models from 2B to 32B parameters. Reasoning amplification improves auditing success in 11 out of 12 settings. The gap between baseline and peak auditing success increases with model scale, suggesting overthinking becomes more effective as models grow. Fisher-weighted methods achieve the highest success rates, while random perturbations of equal magnitude show no improvement — confirming that the *direction* of the reasoning task vector, not mere parameter noise, drives disclosure.

<!-- Placeholder: figure showing auditing success rates across alpha values -->
*[Auditing results figure placeholder]*

## Status

Under review, ICML 2026.

## Co-authors

- [Rowan Wang](/people/rowan-wang)
- [Dipika Khullar](/people/dipika-khullar)
- [Fabien Roger](/people/fabien-roger)
