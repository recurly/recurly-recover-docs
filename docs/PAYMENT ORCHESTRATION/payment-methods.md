---
title: Payment methods
excerpt: >-
  How to supply reusable gateway tokens on a recovery request and use the
  payment method wallet to designate primary and backup methods.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recover collects on a past-due invoice using the payment methods you supply on the recovery request. You pass reusable gateway tokens, and — when the Wallet feature is enabled — designate which method Recover tries first. This page covers supplying a payment method and using the payment method wallet.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available as a standalone product — Recurly Subscriptions is not required</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#supply-a-payment-method"><span class="rp-toc-num">1</span>Supply a payment method</a>
    <a class="rp-toc-pill" href="#payment-method-wallet"><span class="rp-toc-num">2</span>Payment method wallet</a>
  </div>
</div>

# Supply a payment method

Provide each payment method as a reusable gateway token in the `payment_gateway_references` array on a `billing_infos` entry. Each reference carries the `token` and its `reference_type` (for example, `stripe_confirmation_token`). Recover stores the method and uses it to collect on the retry schedule.

For the gateways that issue these tokens, see <a href="https://docs.recurly.com/recurly-recover/docs/payment-gateways" target="_blank">Payment gateways</a>.

# Payment method wallet

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> Designating primary and backup methods requires the Wallet feature to be enabled on your account.</div>
</div>

When the Wallet feature is enabled, you can designate payment methods as primary or backup in the same request. Set `primary_payment_method` or `backup_payment_method` to `true` on each entry in `billing_infos`. You can submit multiple payment methods, but only one can be marked as primary.
