---
title: Retry strategy models
excerpt: >-
  Compare Recurly Recover's default and aggressive retry strategies, including
  the recovery, risk, and account-health trade-offs of each.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recurly Recover offers two retry strategies: a default, network-informed model built for sustainable recovery, and an aggressive opt-in model that trades long-term account health for short-term revenue. Here's how each one works and when to use it.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available on all Recurly plans</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#overview"><span class="rp-toc-num">1</span>Overview</a>
    <a class="rp-toc-pill" href="#default-retry-strategy-recommended"><span class="rp-toc-num">2</span>Default retry strategy</a>
    <a class="rp-toc-pill" href="#aggressive-retry-strategy-opt-in"><span class="rp-toc-num">3</span>Aggressive retry strategy</a>
  </div>
</div>

# Overview

By default, Recurly's retry logic takes its cues from the card networks themselves. We distinguish hard declines (never retried) from soft declines (retry-eligible) to decide whether and when a retry is likely to succeed. This protects your account health with card networks and acquirers, lowering the risk of retry-limit penalties or fraud-pattern flags.

The default strategy is built for sustainable, long-term recovery. The more aggressive strategy is for merchants who prioritize maximum recovery over long-term account health — Recurly can enable it on request. It can recover more revenue in the short term, but it shifts risk to you, including potential network penalties and degraded approval rates over time.

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong>Both strategies produce identical results on short dunning windows of under 20 days. Whichever you choose, we recommend a dunning window of 27 days or longer to give each invoice the best chance of recovery.</div>
</div>

# Default retry strategy (recommended)

Recurly's default retry strategy is gateway- and network-informed, and it uses Recurly's Intelligent Retries machine learning algorithm to time each attempt.

### Pros

<ul class="rp-list">
  <li>Recovers around 98% of the invoices the aggressive model could collect</li>
  <li>Lowers the risk of retry-limit violations and network penalties — Visa and Mastercard both run excessive-retry programs that can trigger fines or account review</li>
  <li>Targets retries using network signals (merchant advice codes, network codes, and decline codes) alongside hard and soft decline classifications, so attempts concentrate where they're likely to succeed</li>
  <li>Preserves a healthier decline-to-approval ratio with acquirers over time</li>
  <li>Reduces the appearance of testing or fraud-like behavior to card issuers</li>
</ul>

### Cons

<ul class="rp-list">
  <li>May delay recovery to standard timelines for merchants who value speed over long-term success</li>
  <li>Slightly lower overall recovery rate</li>
</ul>

# Aggressive retry strategy (opt-in)

The aggressive strategy casts a wider net, retrying transactions the default model would skip. It's opt-in and enabled by Recurly on request.

### Pros

<ul class="rp-list">
  <li>Retries against a broader set of decline codes, attempting transactions the default model won't</li>
  <li>Recovers up to an additional 2% of invoices the default strategy can't reach — worth it when maximizing churn reduction outweighs the risks below</li>
</ul>

### Cons

<ul class="rp-list">
  <li>Risks breaching card-network retry-limit mandates, which can bring per-transaction fines or land you on an acquirer monitoring or remediation plan</li>
  <li>Higher risk of transaction patterns being flagged as adversarial or fraud-like</li>
  <li>Risks a poor customer experience if retries feel excessive — many issuers alert customers to each declined attempt through their card apps, and it's worse if you also notify them yourself</li>
</ul>
