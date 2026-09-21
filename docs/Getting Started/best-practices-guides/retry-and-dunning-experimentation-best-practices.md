---
title: Retry and dunning experimentation best practices
excerpt: >-
  How to design statistically sound experiments when comparing retry and dunning
  configurations in Recurly Recover.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Dunning and retry configurations can significantly affect how many failed payments you recover, but it's rarely obvious which configuration will perform best for your business — recovery depends on customer mix, card types, failure reasons, and more. Running a controlled experiment lets you compare recovery rates between configurations directly, so you know which one actually performs better instead of relying on guesswork or benchmarks that don't reflect your own customers.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available on all Recurly plans</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#why-experimentation-matters"><span class="rp-toc-num">1</span>Why it matters</a>
    <a class="rp-toc-pill" href="#key-considerations"><span class="rp-toc-num">2</span>Key considerations</a>
  </div>
</div>

# Why experimentation matters

Because recovery is a yes-or-no outcome for each invoice, the number of recoveries in a variant behaves like a coin flip repeated many times — some invoices recover and some won't, and the overall rate will naturally shift a bit even when nothing about the underlying performance has changed. Good experiment design accounts for that natural variability, so you can trust that a difference you observe reflects a real difference in performance rather than chance.

# Key considerations

## 1. Random, apples-to-apples variant assignment

Invoices must be assigned to variants randomly. If you group invoices by any non-random criteria — customer segment, card type, or invoice size, for example — differences in recovery rates may reflect those underlying differences rather than the configuration you're testing. True random assignment keeps each variant a fair, comparable sample.

## 2. Setting up variants

Configure experiments by randomly assigning invoices to different dunning campaigns. Once an experiment is running, you can compare variant performance on the Dunning Comparison Dashboard.

## 3. Only use completed invoices

Experimental results are only valid for invoices that have completed their entire dunning cycle. Open invoices — those still being actively retried — haven't yet had the chance to succeed or fail, and including them will distort your results. Exclude every open invoice from your analysis.

## 4. Understanding statistical significance

Whether a result reaches statistical significance depends on several factors: your baseline recovery rate, the size of the impact from the configuration change, and the number of invoices in each variant.

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong>Aim for 10,000 or more invoices per treatment group to maximize your chances of reaching significance for subtle differences of half a percent or less. Bigger effects can reach significance with smaller groups — but treat 500 invoices per variant as a strong minimum.</div>
</div>

We recognize this volume isn't always achievable, especially for smaller merchants. Even without statistical significance, experimentation still provides a useful directional signal, and we encourage merchants to experiment regardless of scale.

***

📋 TODO before publishing:

- [ ] The source ends mid-sentence after "You will be able to recognize" — the rest of this thought (and possibly more content) is missing. Supply the remaining content before publishing.
