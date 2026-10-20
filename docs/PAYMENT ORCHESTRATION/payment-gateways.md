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
  <tr><td>Stripe</td><td>Reusable gateway tokens (for example, <code>stripe_customer</code>) and <code>stripe_payment_method</code></td></tr>
  <tr><td>Braintree</td><td>Legacy gateway tokens or Global IDs</td></tr>
  <tr><td>Adyen</td><td>Reusable gateway tokens + Shopper Reference + NTID</td></tr>
  <tr><td>CommerceHub</td><td>Reusable TransArmor Token + Meta-Data (BIN/4 and Expiry Date) + NTID</td></tr>
  <tr><td>FreedomPay</td><td>Reusable Gateway Token + NTID</td></tr>
</table>

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> Recover collects using reusable tokens only. You pass these tokens per invoice in <code>payment_gateway_references</code> — see <a href="https://docs.recurly.com/recurly-recover/docs/payment-methods" target="_blank">Payment methods</a>.</div>
</div>

# Gateway Configurations

When onboardng each individual gateway, use our guides to help assist with enabling or updating your gateways.&#x20;

<Tabs>
  <Tab title="Adyen">
    See our [primary guide for enabling Adyen in RSM](https://docs.recurly.com/recurly-subscriptions/docs/adyen#adding-adyen-to-your-recurly-site) Documentation. For Recover users, the only required fields are as follows:&#x20;

    * Step 1: select Adyen as a gateway&#x20;
    * Step 2: Add relevant credentials -- username, password, and merchant account details. You do not need to provide an HMAC key or reporting credentials.&#x20;
    * Step 3: Enable payment methods and currencies, and save your configuration.
  </Tab>

  <Tab title="Braintree">
    See our [primary guide for enabling Braintree in RSM](https://docs.recurly.com/recurly-subscriptions/docs/braintree-rd#step-2-configure-braintree-in-recurly) Documentation. For Recover users, the only required fields are as follows:&#x20;

    * Step 1: select Braintree as a gateway&#x20;
    * Step 2: Add relevant credentials -- Input your Merchant ID, Public Key, and Private Key.
    * Step 3: Enable payment methods and currencies, and save your configuration.
  </Tab>

  <Tab title="Commerce Hub">
    See our <Anchor target="_blank" href="https://docs.recurly.com/recurly-subscriptions/docs/commerce-hub#step-3-enter-credentials-in-recurly">primary guide for enabling Commerce Hub in RSM</Anchor> Documentation. For Recover users, the only required fields are as follows:&#x20;

    * Step 1: select Commerce Hub as a gateway&#x20;
    * Step 2: Add relevant credentials -- Fiserv Merchant ID, Terminal ID, API Key, and API Secret. If routing by store or site ID, also enter your Store ID and Site ID. If you are a former Payeezy merchant who was migrated to Commerce Hub, enter your Service Entitlement number as well, otherwise leave this blank.
    * Step 3: Enable payment methods and currencies, and save your configuration.
  </Tab>

  <Tab title="FreedomPay">
    See our <Anchor target="_blank" href="https://docs.recurly.com/recurly-subscriptions/docs/freedompay#step-4-enter-credentials-in-recurly">primary guide for enabling FreedomPay in RSM</Anchor> Documentation. For Recover users, the only required fields are as follows:&#x20;

    * Step 1: select FreedomPay as a gateway&#x20;
    * Step 2: Add relevant credentials -- Store ID, Terminal ID, Enhanced Security Key, Enterprise Code (provided by your FreedomPay representative), and RSA Key ID.
    * Step 3: Enable payment methods and currencies, and save your configuration.
  </Tab>

  <Tab title="Stripe">
    See our <Anchor target="_blank" href="https://docs.recurly.com/recurly-subscriptions/docs/stripe#integrate-stripe-with-recurly">primary guide for enabling Stripe in RSM</Anchor> Documentation. For Recover users, the only required fields are as follows:&#x20;

    * Step 1: select Stripe as a gateway&#x20;
    * Step 2: You will be redirect to Stripe to authenticate, and be redirected back to Recurly. Ensure you are connecting your existing Stripe account rather than creating a new one.
    * Step 3: Credit cards are enabled by default, so enable Apple Pay and Google Pay, and currencies where relevant, and save your configuration.
  </Tab>
</Tabs>

# Gateway codes and routing

Each gateway connection gets a unique **gateway code**. You pass this value in your API requests to route each transaction to the right connection.

To route different card types or gateway tokens through separate accounts, add multiple connections for the same or different providers — each one gets its own gateway code. Pass the matching `gateway_code` on the request to control exactly where a transaction is collected.

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong> Connect and manage gateways in the onboarding flow — see <a href="https://docs.recurly.com/recurly-recover/docs/recurly-recover-overview#getting-started" target="_blank">Getting started</a>.</div>
</div>