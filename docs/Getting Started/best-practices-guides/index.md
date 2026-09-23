---
title: Best practices
excerpt: >-
  Best practices for configuring Recurly Recover — choosing a retry strategy,
  testing recovery invoices, and using single or multiple payment methods.
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recurly Recover gives you several configuration options depending on your use case. Below you'll find best practices for choosing between our standard retry strategy and a more aggressive model, testing your transactions before go-live, and working with single or multiple payment methods. Pick a topic below to get started.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available on all Recurly plans</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#retry-strategies-pros-and-cons"><span class="rp-toc-num">1</span>Retry strategies</a>
    <a class="rp-toc-pill" href="#recover-testing-guides"><span class="rp-toc-num">2</span>Recover testing</a>
    <a class="rp-toc-pill" href="#multiple-payment-methods"><span class="rp-toc-num">3</span>Multiple payment methods</a>
  </div>
</div>

# Retry strategies: pros and cons

Recurly's default retry behavior leans on our gateway partners. We read and respect hard and soft decline indicators, along with merchant advice codes from the card networks, so retries happen when they're most likely to succeed. If you understand the trade-offs, Recurly can also apply a more aggressive retry model on request.

Read up on the pros and cons of each model before you decide.

<div class="rp-nav-grid">

<Cards>
  <Card title="Retry strategy models" href="https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/retry-strategy-models" target="_blank">
    Compare Recurly's standard retry strategy with the more aggressive model, and weigh the trade-offs of each.
  </Card>
</Cards>
</div>

# Recover testing guides

Testing is a key part of enabling Recurly Recover. Follow the guides below to set up recovery invoices on your sandbox site before go-live.

Whatever your setup or use case, use Recurly's custom descriptors so the descriptors on the transactions you run in your own environment match what Recurly sends through our integrations.

<div class="rp-nav-grid">

<Cards>
  <Card title="Single payment method, single or multiple gateways" href="https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/single-payment-method-single-multi-gateway" target="_blank">
    Set up and test recovery when subscribers use one payment method across one or more gateways.
  </Card>
  <Card title="Multi-payment method, single gateway" href="https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/multi-payment-method-single-gateway" target="_blank">
    Configure and test recovery for multiple payment methods routed through a single gateway.
  </Card>
  <Card title="Multi-payment method, multi-gateway" href="https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/multi-payment-method-multi-gateway" target="_blank">
    Test recovery when multiple payment methods are spread across multiple gateways.
  </Card>
</Cards>
</div>

# Multiple payment methods

You can add multiple payment methods to a recovery invoice. This raises the odds of collecting the invoice, and it lets you keep the same payment method in tokenized form when you're using multiple gateways.

Learn the best practices for multiple payment methods, multiple gateways, and how Recurly Wallet supports this setup.

<div class="rp-nav-grid">

<Cards>
  <Card title="Multiple payment methods best practices" href="https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/multiple-payment-methods" target="_blank">
    See how multiple payment methods and Recurly Wallet work together to improve recovery rates.
  </Card>
</Cards>
</div>
