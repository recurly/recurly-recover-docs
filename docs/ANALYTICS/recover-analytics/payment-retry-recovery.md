---
title: Payment retry recovery
excerpt: >-
  Track revenue recovered through intelligent retries and see how recoveries
  break down across retry attempts in the Payment Retry Recovery dashboard.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Monitor retained revenue through intelligent retry strategies, and track how optimized retry logic recovers payments that initially failed. Across Recurly's network, the majority of recovered transactions happen within the first several retry attempts, so this dashboard shows you exactly where your recoveries are coming from.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#filters"><span class="rp-toc-num">1</span>Filters</a>
    <a class="rp-toc-pill" href="#key-metrics"><span class="rp-toc-num">2</span>Key metrics</a>
    <a class="rp-toc-pill" href="#charts"><span class="rp-toc-num">3</span>Charts</a>
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

Each metric is compared against the previous equivalent period, with the change shown as a percentage.

<table class="rp-params">
  <tr class="rp-thead-row"><td>Metric</td><td>Description</td></tr>
  <tr><td>Recovered Transactions</td><td>The count of failed payments successfully processed again through the retry engine during the selected period.</td></tr>
  <tr><td>Retry Attempts</td><td>The total number of payments retried in the period.</td></tr>
  <tr><td>Revenue at Risk</td><td>The total dollar value of all invoices whose first payment failed during the period.</td></tr>
  <tr><td>Payment Retry Recovered Revenue</td><td>Total revenue recovered through successful retries, including intelligent retries, Account Updater, payment method updates, and third parties that report recovery back to Recurly.</td></tr>
  <tr><td>Recovery Rate</td><td>The percentage of at-risk revenue successfully recovered in the period.</td></tr>
</table>

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong>Failures and recoveries are tracked as independent trends and aren't matched on a per-invoice basis. Recovery Rate reflects overall recovery health rather than a precise per-invoice cohort rate, so it won't always equal Recovered Revenue divided by Revenue at Risk.</div>
</div>


<Image src="https://files.readme.io/ee80a918e8f8f2aa1e84761d2e6b06d966a9a6b3120e1b5cda51d11da51a263c-image.png" border={true} />


# Charts

### Payment recovery over time

This chart shows recovered transactions across the selected date range, so you can spot spikes, dips, and trends in your recovery performance over time.


<Image src="https://files.readme.io/01e7636ef834df7c53d18cf003ab302b2b996ebd024364b65ac27ac8e0dd3dc8-image.png" border={true} />


### Success by retry attempt number

This chart shows how many transactions were recovered at each retry attempt number. Recoveries concentrate in the earliest attempts and taper off across later ones, showing you where your retry logic is doing the most work.


<Image src="https://files.readme.io/0d849411d92dfb9d8b2c31732fe088902ee506b34bd1bc6fedd7ddbdce958e13-image.png" border={true} />


<br />

<br />
