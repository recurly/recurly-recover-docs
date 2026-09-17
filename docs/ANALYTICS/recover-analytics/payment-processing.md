---
title: Payment processing
excerpt: >-
  Monitor payment success rates and decline patterns across payment methods,
  gateways, and card BINs in the Payment Processing dashboard.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Get a granular view of payment success rates across payment methods, gateways, and card Bank Identification Numbers (BINs). Monitor success rates and decline patterns to spot underperformance fast and optimize how payments flow through your stack.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#filters"><span class="rp-toc-num">1</span>Filters</a>
    <a class="rp-toc-pill" href="#key-metrics"><span class="rp-toc-num">2</span>Key metrics</a>
    <a class="rp-toc-pill" href="#charts"><span class="rp-toc-num">3</span>Charts</a>
    <a class="rp-toc-pill" href="#tables"><span class="rp-toc-num">4</span>Tables</a>
  </div>
</div>

# Filters

<table class="rp-params">
  <tr class="rp-thead-row"><td>Filter</td><td>Description</td></tr>
  <tr><td>Date Range</td><td>The reporting period. Defaults to the past 30 days.</td></tr>
  <tr><td>Payment Method</td><td>Filters by card or alternative payment type (Credit Card, Debit Card, PayPal, and more).</td></tr>
  <tr><td>Gateway</td><td>Filters by payment gateway.</td></tr>
</table>

# Key metrics

**Overall Success Rate** — the percentage of transactions that succeeded across both customer- and merchant-initiated payments during the selected period, compared against the previous equivalent period.


<Image src="https://files.readme.io/a84c021f8c9dbd38ca5ad54aeb4cc2446c76aac08bc0001e83f48a1ece7f42bc-image.png" align="center" width="80%" border={true} />


# Charts

### Payment success rate over time

This chart shows your transaction success rate across the selected date range, so you can track performance trends and identify periods where success dipped.


<Image src="https://files.readme.io/f00ffb929c3868199afa5729866b56d9511ace24ad1342fa12d48b89bdaf66c4-image.png" align="center" border={true} />


### Payment method distribution

This chart shows the relative share of transaction volume by payment method, so you can see which methods your customers use most.


<Image src="https://files.readme.io/47f33443f5f75be90fc127f4b6b6020fa35c981a6d18847f1b65857f4253c985-image.png" align="center" width="85%" border={true} />


### Gateway success rate

This chart shows the successful transaction percentage for each payment gateway side by side, so you can compare authorization performance across your gateways.


<Image src="[TODO: add image — Gateway Success Rate chart]" align="center" width="75%" border={true} />


# Tables

### Payment Method Success Rate

Breaks down performance by payment method, showing the transaction count, successful transaction count, and successful transaction percentage for each.


<Image src="[TODO: add image — Payment Method Success Rate table]" align="center" width="75%" border={true} />


### IIN & Issuer Success Rate

Shows authorization performance by card BIN — the Issuer Identification Number (IIN) that identifies the issuing bank — alongside the payment method, country, transaction count, successful transaction count, and successful transaction percentage. Use it to identify underperforming issuers.


<Image src="[TODO: add image — IIN & Issuer Success Rate table]" align="center" width="75%" border={true} />


### Payment Decline Reasons

Ranks the reasons transactions failed, categorized as hard, soft, or fraud declines, with the count for each failure type. Soft declines often represent recoverable revenue through retries or account updates, while hard declines signal issues that require more targeted intervention.


<Image src="[TODO: add image — Payment Decline Reasons table]" align="center" width="75%" border={true} />


***

📋 TODO before publishing:

- [ ] Add image — Overall Success Rate tile
- [ ] Add image — Payment Success Rate Over Time chart
- [ ] Add image — Payment Method Distribution chart
- [ ] Add image — Gateway Success Rate chart
- [ ] Add image — Payment Method Success Rate table
- [ ] Add image — IIN & Issuer Success Rate table
- [ ] Add image — Payment Decline Reasons table
