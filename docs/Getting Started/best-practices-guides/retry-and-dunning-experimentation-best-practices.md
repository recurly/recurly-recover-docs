---
title: Retry and dunning experimentation best practices
deprecated: false
hidden: true
metadata:
  robots: index
---
# Best Practices for Configuring Retry Recovery Rate Experiments

## Why Experimentation Matters

Dunning and retry configurations can significantly affect how many failed payments get recovered. But it's not always obvious which configuration will perform best for a given merchant — recovery rates depend on customer mix, card types, failure reasons, and more. Running a controlled experiment lets you compare recovery rates between different configurations (variants) directly, so you can determine which one actually performs better rather than relying on guesswork or unrelated benchmarks.

Because recovery is a yes/no outcome for each invoice, the number of recoveries in a variant behaves like a coin flip repeated many times — some invoices will recover and some won't, and the overall rate will naturally vary a bit even if nothing about the underlying performance has changed. Good experiment design accounts for this natural variability so you can be confident that a difference you observe reflects a real difference in performance, not just chance.

## Key Considerations

### 1. Random, Apples-to-Apples Variant Assignment

Invoices must be assigned to variants randomly. If invoices are grouped by any non-random criteria (for example, by customer segment, card type, or invoice size), differences in recovery rates may reflect those underlying differences rather than the configuration being tested. True random assignment ensures each variant is a fair, comparable sample.

### 2. Setting Up Variants

Merchants configure experiments by randomly assigning invoices to different dunning campaigns. Once an experiment is running, performance comparisons across variants are available on the Dunning Comparison Dashboard.

### 3. Only Use Completed Invoices

Experimental results are only valid for invoices that have completed their entire dunning cycle. Open invoices — those still actively being retried — have not yet had the chance to succeed or fail, and including them will distort the results. Exclude all open invoices from experimental analysis.

### 4. Understanding Statistical Significance

Whether a result reaches statistical significance depends on several factors:

- The baseline recovery rate
- The size of the impact from the configuration change
- The number of invoices in each variant

**We ideally recommend 10,000 or more invoices per treatment group** to maximize the likelihood of reaching a statistically significant result for subtle differences of half a percent or less.  You will be able to reach statistical significance with smaller groups if your changes have a bigger effect.  **A bare minimum of 500 invoices is strongly recommended for each variant.**

We recognize this volume isn't always achievable, especially for smaller merchants. Even without statistical significance, experimentation still provides a useful directional signal, and we encourage merchants to experiment regardless of scale.  You will be able to recognize&#x20;
