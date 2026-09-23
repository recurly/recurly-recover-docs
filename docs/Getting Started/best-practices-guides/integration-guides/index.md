---
title: Integration and testing
excerpt: >-
  Testing best practices and use-case guides for going live with Recurly
  Recover's retry strategies.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Follow the standard Recurly go-live checklist like any other merchant, then layer on a few testing behaviors specific to Recover's retry strategies before you flip the switch on live traffic.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available on all Recurly plans</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#overview"><span class="rp-toc-num">1</span>Overview</a>
    <a class="rp-toc-pill" href="#best-practices"><span class="rp-toc-num">2</span>Best practices</a>
    <a class="rp-toc-pill" href="#use-case-testing-guides"><span class="rp-toc-num">3</span>Use-case guides</a>
  </div>
</div>

# Overview

Before you go live, work through the standard Recurly go-live checklist like any other merchant. Because you're using Recover's <a href="https://docs.recurly.com/recurly-recover/docs/retry-strategy-models" target="_blank">retry strategies</a>, build a few extra testing behaviors into your rollout first.

# Best practices

<ul class="rp-list">
  <li><strong>Start small</strong> — send a small percentage of your overall volume first to confirm your live traffic is flowing correctly</li>
  <li><strong>Ramp up gradually</strong> — increase volume on your own timeline, and let the data drive each step</li>
  <li><strong>Run multiple dunning campaigns</strong> — split customers into cohorts so you can compare recovery rates across statistically distinct groups</li>
  <li><strong>Test different campaign durations</strong> — try extending your retry window to see whether it captures more long-tail recoveries</li>
  <li><strong>Tailor testing to your setup</strong> — the right approach depends on your payment method and gateway combination. One or more of the use cases below may apply, depending on your customer data and the gateways you enable.</li>
</ul>

# Use-case testing guides

Your testing approach depends on your payment method and gateway mix. Follow the guide that matches your use case:

<div class="rp-nav-grid">

<Cards>
  <Card title="Single payment method, single gateway" href="https://docs.recurly.com/recurly-recover/docs/single-payment-method-single-multi-gateway" target="_blank">
    Test recovery when subscribers use a single payment method.
  </Card>
  <Card title="Multi-payment method, single gateway" href="https://docs.recurly.com/recurly-recover/docs/multi-payment-method-single-gateway" target="_blank">
    Test recovery for multiple payment methods routed through one gateway.
  </Card>
  <Card title="Multi-payment method, multi-gateway" href="https://docs.recurly.com/recurly-recover/docs/multi-payment-method-multi-gateway" target="_blank">
    Test recovery when multiple payment methods are spread across multiple gateways.
  </Card>
</Cards>
</div>
