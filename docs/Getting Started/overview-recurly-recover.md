---
title: 'Overview: Recurly Recover'
excerpt: >-
  Use Recurly Recover's standalone retry engine to collect on past-due invoices
  from your existing billing platform — without adopting Recurly for
  subscription management.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recurly Recover is a standalone retry engine for collecting on past-due invoices without adopting Recurly as your primary billing platform. Submit a failed invoice through the Recovery API, and Recurly automatically creates the account objects, calculates an optimized retry schedule, and manages the entire collection lifecycle until the invoice is paid or the retry window closes.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available as a standalone product — Recurly Subscriptions is not required</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#key-benefits"><span class="rp-toc-num">1</span>Key benefits</a>
    <a class="rp-toc-pill" href="#how-recurly-recover-works"><span class="rp-toc-num">2</span>How it works</a>
    <a class="rp-toc-pill" href="#before-you-begin"><span class="rp-toc-num">3</span>Before you begin</a>
    <a class="rp-toc-pill" href="#getting-started"><span class="rp-toc-num">4</span>Getting started</a>
    <a class="rp-toc-pill" href="#in-this-section"><span class="rp-toc-num">5</span>In this section</a>
    <a class="rp-toc-pill" href="#faqs"><span class="rp-toc-num">6</span>FAQs</a>
  </div>
</div>

# Limitations

<ul class="rp-list">
  <li>Recurly Recover is designed for merchants who don't use Recurly for subscription management.</li>
  <li>Each successful API call creates one account with one invoice. Calling the API again with the same account code returns an error.</li>
  <li>Accounts can only be created through the API, not through the Admin UI.</li>
  <li>Merchants who already use Recurly Subscriptions should use the retry logic built into Recurly Subscriptions instead.</li>
</ul>

# Key benefits

<div class="rp-benefits rp-benefits-2x2">
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-plug" aria-hidden="true"></i></div>
    <strong>Works with your stack</strong>
    <span>Use Recurly's retry engine without adopting Recurly for subscription management — it plugs into your existing billing system.</span>
  </div>
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-sliders" aria-hidden="true"></i></div>
    <strong>Flexible retry strategies</strong>
    <span>Assign a different dunning campaign per API request, so you can A/B test retry windows and strategies across customer segments.</span>
  </div>
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-arrows-rotate" aria-hidden="true"></i></div>
    <strong>Fully managed collection</strong>
    <span>Recurly handles the entire retry lifecycle — calculating optimal retry dates, managing payment attempts, and firing webhooks when the journey ends.</span>
  </div>
  <div class="rp-benefit">
    <div class="rp-benefit-icon"><i class="fa-solid fa-bolt" aria-hidden="true"></i></div>
    <strong>Minimal setup</strong>
    <span>No plans, items, or taxes to configure. Setup is limited to your payment gateway, a retry window, and the API integration.</span>
  </div>
</div>

# How Recurly Recover works

<div class="rp-steps">
  <div class="rp-step">
    <div class="rp-step-num">1</div>
    <div><h4>A payment fails</h4><p>A charge fails on your billing platform.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">2</div>
    <div><h4>Pause your internal retries</h4><p>You pause your own retry logic for that invoice so Recover is the only system attempting collection.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">3</div>
    <div><h4>Submit the invoice to Recover</h4><p>You call the Recovery API with account details, payment method tokens, prior attempt history, and the retry window you want Recurly to use.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">4</div>
    <div><h4>Recurly builds the records</h4><p>Recurly creates an account, a past-due invoice, and a failed transaction.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">5</div>
    <div><h4>Retries begin</h4><p>Recurly calculates the first retry date from your submission and starts retrying on the assigned retry window.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">6</div>
    <div><h4>Recover fires a webhook</h4><p>When a retry succeeds or the retry window is exhausted, Recurly fires a webhook so you can update the invoice state in your system.</p></div>
  </div>
</div>

<div class="rp-callout rp-callout-warning">
  <div><strong><i class="fa-solid fa-triangle-exclamation" aria-hidden="true"></i> Warning</strong> Pause your internal retry logic before submitting an invoice to Recurly Recover. Running parallel retries on the same payment method risks double-charging your customer.</div>
</div>

# Before you begin

You'll need the following in place to start collecting with Recurly Recover:

<ul class="rp-list">
  <li>An active Recurly Recover account with an API key generated.</li>
  <li>At least one retry window (dunning campaign) configured.</li>
</ul>

# Getting started

The first time you sign in, Recurly walks you through configuration.

<div class="rp-steps">
  <div class="rp-step">
    <div class="rp-step-num">1</div>
    <div><h4>Connect your payment gateway</h4><p>In the onboarding flow, click <strong>Add Gateway</strong> and follow the prompts to connect your gateway. Add as many gateways as you need, then click <strong>Continue</strong> to move on.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">2</div>
    <div><h4>Note the gateway code</h4><p>Each gateway connection gets a unique <strong>gateway code</strong>. You'll pass this value in your API requests to route transactions to the right gateway. To route different card types or merchant category codes through separate accounts, add multiple connections for the same provider — each one gets its own gateway code.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">3</div>
    <div><h4>Set up webhooks</h4><p>Enter your <strong>Endpoint URL</strong> and select the events you want Recover to send. See <a href="/docs/recurly-recover-webhooks" target="_blank">Webhooks</a> for the full event reference.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">4</div>
    <div><h4>Copy your API key</h4><p>Copy <strong>Your API key</strong> from the onboarding flow — you'll need it to authenticate every Recovery API request.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">5</div>
    <div><h4>Make your first API call</h4><p>Head to <a href="/docs/recurly-recover-recovery-api" target="_blank">Submit invoices via the Recovery API</a> to send your first failed invoice for collection.</p></div>
  </div>
</div>

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> Recover currently supports <strong>Stripe</strong> and <strong>Braintree</strong> with reusable gateway tokens. <a href="/docs/recurly-recover-recovery-api" target="_blank">Learn more</a> about gateways and token support.</div>
</div>

# In this section

<div class="rp-nav-grid">

<Cards>
  <Card title="Submit invoices via the Recovery API" href="/docs/recurly-recover-recovery-api" target="_blank">
    Send a failed invoice for collection, read the response, and stop retries when a payment is collected elsewhere.
  </Card>
  <Card title="Webhooks" href="/docs/recurly-recover-webhooks" target="_blank">
    Track retry progress and confirm final outcomes with Recover's four webhook events.
  </Card>
  <Card title="Roles & permissions" href="/docs/recurly-recover-roles-permissions" target="_blank">
    Create roles and control who can reach configuration, integrations, and analytics.
  </Card>
</Cards>
</div>

# FAQs

<Accordion title="Do I need Recurly Subscriptions to use Recurly Recover?" icon="fa-solid fa-link-slash">
  No. Recurly Recover is a standalone retry engine for merchants using other billing platforms. Combining Recurly Recover with Recurly Subscriptions is not recommended.
</Accordion>

<Accordion title="Can I use Recurly Recover with existing Recurly Subscriptions customers?" icon="fa-solid fa-ban">
  Recurly Recover isn't intended to run alongside Recurly Subscriptions — payment recovery is already included in your Recurly Subscriptions plan. For help deciding which solution fits, contact Recurly Sales or email <a href="mailto:support@recurly.com" target="_blank">[support@recurly.com](mailto:support@recurly.com)</a>.
</Accordion>

<Accordion title="What happens when I submit a past-due invoice via the API?" icon="fa-solid fa-file-invoice">
  Recurly creates an account (with no subscription), a charge invoice, and one or more failed transactions. Your billing information is stored, and Recurly automatically calculates the next collection attempt based on your submission. See <a href="/docs/recurly-recover-recovery-api" target="_blank">Submit invoices via the Recovery API</a> for the full request and response.
</Accordion>

{/*
📋 TODO before publishing:
- [ ] Plan pill wording — confirm the commercial framing for Recover (e.g. plan name, "contact Sales" language). Current pill states only that Subscriptions isn't required, which the source supports.
- [ ] Internal slugs — replace every /docs/recurly-recover-* href (the three nav cards, Getting started steps 3 and 5, and the last FAQ) with the real ReadMe slugs once the spoke pages exist.
- [ ] "Learn more" gateway/token link — confirm where the supported-gateways note in Getting started should point (Recovery API page vs. a general Recurly gateways doc). Currently points to the Recovery API page.
*/}
