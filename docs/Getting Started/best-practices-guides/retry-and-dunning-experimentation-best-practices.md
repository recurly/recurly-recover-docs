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

<div class="rp-nav-grid">

<Cards>
  <Card title="1. Random, apples-to-apples variant assignment">
    Assign invoices to variants randomly. Grouping by customer segment, card type, or invoice size instead can make your results reflect those differences rather than the configuration you're testing.
  </Card>
  <Card title="2. Setting up variants">
    Configure experiments by randomly assigning invoices to different dunning campaigns, then compare variant performance on the Dunning Comparison Dashboard.
  </Card>
  <Card title="3. Only use completed invoices">
    Only analyze invoices that have completed their full dunning cycle — open invoices haven't yet succeeded or failed, and including them will distort your results.
  </Card>
  <Card title="4. Understanding statistical significance">
    Significance depends on your baseline recovery rate, the size of the change's impact, and how many invoices are in each variant.
  </Card>
</Cards>
</div>

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong>Aim for 10,000 or more invoices per treatment group to maximize your chances of reaching significance for subtle differences of half a percent or less. Bigger effects can reach significance with smaller groups — but treat 500 invoices per variant as a strong minimum.</div>
</div>

We recognize this volume isn't always achievable, especially for smaller merchants. Even without statistical significance, experimentation still provides a useful directional signal, and we encourage merchants to experiment regardless of scale.

***

📋 TODO before publishing:

- [ ] The source ends mid-sentence after "You will be able to recognize" — the rest of this thought (and possibly more content) is missing. Supply the remaining content before publishing.
