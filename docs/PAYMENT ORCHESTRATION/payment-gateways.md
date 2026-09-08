---
title: Payment gateways
excerpt: >-
  The payment gateways Recurly Recover supports for retry collection, how
  gateway codes route transactions, and the reusable tokens Recover requires.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recover routes every retry transaction through a payment gateway you connect during onboarding. Each connection is identified by a gateway code that you pass in your API requests, and Recover collects using reusable tokens issued by that gateway. This page covers the supported gateways, how gateway codes route transactions, and the tokens Recover needs.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available as a standalone product — Recurly Subscriptions is not required</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#supported-gateways"><span class="rp-toc-num">1</span>Supported gateways</a>
    <a class="rp-toc-pill" href="#gateway-codes-and-routing"><span class="rp-toc-num">2</span>Gateway codes and routing</a>
  </div>
</div>

# Supported gateways

Recover currently supports the following gateways, each with reusable gateway tokens:

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Gateway</td><td>Token support</td></tr>
  <tr><td>Stripe</td><td>Reusable gateway tokens (for example, <code>stripe_confirmation_token</code>)</td></tr>
  <tr><td>Braintree</td><td>Reusable gateway tokens</td></tr>
</table>

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> Recover collects using reusable tokens only. You pass these tokens per invoice in <code>payment_gateway_references</code> — see <a href="https://docs.recurly.com/recurly-recover/docs/payment-methods" target="_blank">Payment methods</a>.</div>
</div>

# Gateway codes and routing

Each gateway connection gets a unique **gateway code**. You pass this value in your API requests to route each transaction to the right connection.

To route different card types or merchant category codes through separate accounts, add multiple connections for the same provider — each one gets its own gateway code. Pass the matching `gateway_code` on the request to control exactly where a transaction is collected.

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong> Connect and manage gateways in the onboarding flow — see <a href="https://docs.recurly.com/recurly-recover/docs/recurly-recover-overview#getting-started" target="_blank">Getting started</a>.</div>
</div>
