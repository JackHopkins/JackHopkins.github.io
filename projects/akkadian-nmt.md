---
layout: page
title: "Akkadian to English NMT"
---

Neural machine translation of ancient cuneiform

---

Akkadian is one of the oldest known written languages, used across Mesopotamia for over two millennia and preserved on hundreds of thousands of clay tablets. Despite this vast corpus, only a fraction of surviving texts have been translated, because the bottleneck is the small number of trained Assyriologists worldwide. This project builds a neural machine translation system to help bridge that gap, translating Akkadian cuneiform into English.

The core idea is to apply test-time compute to ancient language translation. Rather than training on raw transliteration-translation pairs, we use Claude Opus to generate detailed reasoning chains that mechanistically decompose each translation. Opus is given a lexicon, grammar reference, logography, and parallel translations, and produces structured (transliteration, reasoning, translation) tuples following a three-stage pipeline: **GLOSS** parses each token, identifying logograms, bound morphemes, and determinatives and mapping them to their Akkadian readings and English meanings; **COMPOSE** builds noun phrases, verb phrases, and clauses, annotating grammatical function (stem, tense, person, case); and **ASSEMBLE** composes the final English translation from the parsed components.

We distill these on-policy, keeping only high-scoring examples where the reasoning is "load-bearing." The filtering criterion is strict: if Opus cannot mechanistically map the transliteration to the target translation without introducing unbounded terms, meaning words that aren't justified by the source and lexicon, the example is discarded. Starting from 140,689 lines in the [ORACC](http://oracc.org/) corpus, we filtered down to ~26,000 training pairs (under 20%), using data quality as a feature rather than a cost. The model is prompted with the source dialect (currently Neo-Assyrian) to disambiguate terms that differ across dialects, and the final model is a full-parameter fine-tune of Qwen3-4B, [available on HuggingFace](https://huggingface.co/Noddybear/akkadian-qwen3-4b).

## Results

The best model achieves **63.26 BLEU** and **74.44 chrF++** on the validation set. Test set evaluation is ongoing.

| Model | BLEU | chrF++ |
|-------|------|--------|
| Qwen3-4B + enriched reasoning (v5) | **63.26** | **74.44** |
| Qwen3-4B + enriched reasoning (v2) | 52.13 | 67.65 |
| Qwen3-4B + enriched reasoning (v3) | 44.98 | 62.32 |
| Qwen3-4B + enriched reasoning (v1) | 39.28 | 58.33 |
| Qwen3-1.7B + enriched reasoning (v5) | 37.07 | 55.88 |
| Qwen3-4B baseline (no reasoning) | 36.53 | 50.84 |

The reasoning traces nearly double BLEU compared to the baseline without them (63.26 vs 36.53), confirming that the chains are load-bearing. The model doesn't just memorise translations, it learns to reason about the language.

## Example

**Input (Neo-Assyrian transliteration):**

`LUGAL KUR—aš-šur {KI} EN-i-ni ni-šap-par-uš tab-bi-x+x ma-aṣ-ṣar-tu₂ ša₂ {1}-AN.ŠAR₂—DU₃—DUMU.UŠ`

**Reasoning chain (abbreviated):**

> **GLOSS**: LUGAL → "king"; KUR—aš-šur → "of Assyria"; EN-i-ni → "our lord" (bēlu + 1cp possessive); ni-šap-par-uš → "we send to him" (G-stem present 1cp + 3ms dative suffix); tab-bi-x+x → "\<gap\>" (damaged signs); ma-aṣ-ṣar-tu₂ → "the watch/guard"; AN.ŠAR₂—DU₃—DUMU.UŠ → "Assurbanipal"
>
> **COMPOSE**: NP1: "king of Assyria" ← royal title with GN genitive complement. VP1: "we send to him" ← ni-šappar + dative -uš. NP3: "the watch of Assurbanipal" ← maṣṣartu + ša-genitive + PN.
>
> **ASSEMBLE**: Combine with Akkadian OBJ-V word order reflected.

**Output:**

King of Assyria, our lord, we send to him \<gap\> the watch of Assurbanipal.

Note the `<gap>` marker for damaged signs (`tab-bi-x+x`). This behaviour emerged naturally: because the reasoning chain must mechanistically justify each translated term from the source, the model learns to mark broken signs rather than hallucinate content for them.
