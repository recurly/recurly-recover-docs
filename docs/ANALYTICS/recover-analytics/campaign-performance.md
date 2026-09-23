---
title: Campaign performance
excerpt: >-
  Compare recovery performance across retry windows to see which strategies
  recover the most revenue in the Campaign Performance dashboard.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Compare recovery performance across multiple retry windows so you can see which strategies work best. This dashboard is built for Recover customers who A/B test retry approaches across different customer segments or invoice types.</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#filters"><span class="rp-toc-num">1</span>Filters</a>
    <a class="rp-toc-pill" href="#charts"><span class="rp-toc-num">2</span>Charts</a>
  </div>
</div>

# Filters

<table class="rp-params">
  <tr class="rp-thead-row"><td>Filter</td><td>Description</td></tr>
  <tr><td>Date Range</td><td>The reporting period. Defaults to the past 18 months.</td></tr>
  <tr><td>Retry Window</td><td>Filters to one or more retry windows.</td></tr>
  <tr><td>Invoice Collection Method</td><td>Filters by how the invoice is collected, such as automatic or manual. Defaults to Automatic.</td></tr>
</table>

# Charts

### Recovery by retry window

This chart shows the recovery rate for each retry window, so you can compare how your campaigns perform against one another. The accompanying table breaks each retry window down further with these columns:

<table class="rp-params">
  <tr class="rp-thead-row"><td>Column</td><td>Description</td></tr>
  <tr><td>Invoices Created</td><td>The number of invoices generated during the period.</td></tr>
  <tr><td>Entered Dunning</td><td>The number of invoices that went past due and entered a retry window.</td></tr>
  <tr><td>Recovered</td><td>The number and percentage of past-due invoices that were successfully collected.</td></tr>
  <tr><td>Still Past Due</td><td>The number and percentage of invoices that remain unpaid and are still in an active retry window.</td></tr>
  <tr><td>Not Recovered</td><td>The number and percentage of invoices that were not collected.</td></tr>
  <tr><td>Successful Retries</td><td>Invoices recovered through Recurly Recover's intelligent retries.</td></tr>
</table>


<Image src="https://files.readme.io/7f47a9b203ac47f39c143ffa1537508945780ddf0911ab8db2820c9f3d7bd241-image.png" border={true} />



<Image src="https://files.readme.io/86acc203378b33c2257a4445d0247c792fdb1ff880b59e9b252f92c746ec2c4b-image.png" border={true} />


### Recovery by day

This chart shows how many invoices were recovered on each day in the retry window, broken out by retry window, so you can see how quickly each campaign recovers revenue. The accompanying table lists, for each day in the retry window, the recovered invoice count and percent recovered per retry window.


<Image src="https://files.readme.io/da3aae0a30c2769fe6ac9e191ac454e17d6a1a0455ee168429c57fc5f7d7d6da-image.png" border={true} />



<Image src="https://files.readme.io/3ed960f926ec9236012afb8bf8772c8e66be3195b6eb2621de8b4d54f47daba8-image.png" border={true} />


<br />

<br />
