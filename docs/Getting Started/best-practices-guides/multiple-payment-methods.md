---
title: Multiple payment ethods
excerpt: >-
  Best practices for adding multiple payment methods to recovery invoices with
  Recurly Wallet, including gateway token and configuration requirements.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recover turns on Recurly Wallet by default, so you can store one or many payment methods on a recovery invoice. Adding a backup method is one of the simplest ways to lift your recovery rate — here's how to do it well.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available on all Recurly plans</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#overview"><span class="rp-toc-num">1</span>Overview</a>
    <a class="rp-toc-pill" href="#best-practices"><span class="rp-toc-num">2</span>Best practices</a>
    <a class="rp-toc-pill" href="#set-up-for-success"><span class="rp-toc-num">3</span>Set up for success</a>
  </div>
</div>

# Overview

Recurly Recover turns on Recurly Wallet for every site by default, so you can store one or many payment methods on a recovery invoice. A customer with a single card on file is exposed to any decline — an expired or reissued card, or even a temporary hold, can stall an invoice's recovery. Adding a backup method closes that gap.

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong>Invoices with two or more payment methods on file see a 40% boost in recovery rates — storing a backup is one of the highest-leverage changes you can make.</div>
</div>

# Best practices

<ul class="rp-list">
  <li><strong>Encourage customers to add a second payment method proactively</strong> — at signup or in account settings, not just after a failed charge. When you send recovery invoices to Recurly, include every method so we can retry against any the customer has provided.</li>
  <li><strong>Favor variety over duplicates</strong> — an Apple Pay token built on the same card number (PAN) adds little protection. A different card network, or PayPal backed by a bank account or PayPal balance, is far more resilient.</li>
  <li><strong>Keep backup methods current</strong> — expired or removed backups give no real coverage. When a customer adds a new method to your wallet system, pass that detail to Recurly, and periodically nudge customers to remove expired or unused cards.</li>
  <li><strong>Be transparent that a backup may be charged if the primary fails</strong> — so a successful backup charge is never a surprise</li>
  <li><strong>Let customers pick their preferred primary</strong> — some want control over which method absorbs a failed charge. Use Recurly Wallet's primary and backup designations to mirror those preferences.</li>
</ul>

# Set up for success

To get the most out of multiple payment methods, make sure the following are in place before you send recovery invoices.

### Validate your gateway tokens

Make sure you have a gateway token for each payment method, with the correct `gateway_code` matched to that token's gateway. Gateway tokens are usually tied to a specific gateway account (with few exceptions), so a mismatched code can cause an error. To retry the same payment method across more than one gateway, include a token for that method for every gateway you want us to attempt — and add each of those gateways to your site. Depending on the gateway, you may also need to provide the expiration date and the Network Transaction ID (NTID) you keep on file for the customer's subscription.

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong>NTID provisioning isn't required for Stripe, Braintree, or PayPal Complete.</div>
</div>

### Enable token backfilling

If you don't have the metadata (first six, last four, and card brand) for your tokens, Recurly can query your gateway for up-to-date card brand, BIN, and expiration data when the gateway requires it for processing. In some cases you'll need to enable specific permissions at the gateway level for this to work.

### Follow the guide for your use case

Your exact setup depends on whether your payment methods live on one gateway or several. Follow the guide that matches your use case:

<div class="rp-nav-grid">

<Cards>
  <Card title="Multiple payment methods, single gateway" href="https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/multi-payment-method-single-gateway" target="_blank">
    Configure and test recovery for several payment methods routed through a single gateway.
  </Card>
  <Card title="Multiple payment methods, multiple gateways" href="https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/multi-payment-method-multi-gateway" target="_blank">
    Set up and test recovery when payment methods are spread across multiple gateways.
  </Card>
</Cards>
</div>
