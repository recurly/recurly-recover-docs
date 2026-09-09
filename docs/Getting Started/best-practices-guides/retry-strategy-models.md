---
title: Retry strategy models
excerpt: >-
  Review our retry strategy pro and con list, and ensure you're using the
  strategy that's right for your business needs and risk level.
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
# Overview&#x20;

By default, Recurly's retry logic is informed by the card networks themselves — we distinguish hard declines (no retry) from soft declines (retry-eligible), and we read Merchant Advice Codes from Visa, Mastercard, and other networks to decide whether and when a retry is likely to succeed. This approach protects your account health with card networks and acquirers, reducing the risk of retry-limit penalties or fraud-pattern flags.

For merchants who prioritize maximum recovery over account health over time, Recurly can enable a more aggressive retry strategy on request. This can recover more revenue in the short term, but shifts risk to the merchant — including potential network penalties and degraded approval rates over time.

Our default strategy is built for sustainable, long-term recovery, while our more aggressive strategy is available for merchants who understand and accept the tradeoffs.

## &#x20;Default Retry Strategy (Recommended)

Recurly's default retry model is gateway- and network-informed, using Recurly’s Intelligent Retries machine learning algorithm to inform retry timing.

**Pros**

- Recovers around 98% of all invoices that the aggressive model could collect.
- Lower risk of retry-limit violations or network penalties (Visa and Mastercard both enforce excessive-retry programs that can result in fines or account review)
- Retries are targeted using network-provided signals (merchant advice codes) and hard/soft decline classifications, so retry attempts are concentrated where they’re likely to succeed.
- Preserves a healthier decline/approval ratio with acquirers over time
- Reduces appearance of looking like ‘testing’ behavior or fraud-like behavior with Issuers.

**Cons**

- For merchants where speed matters more than long-term success, this model can delay success to standard timelines.
- Merchants who retry hard-declines in their own environments won’t find the same level of success with this model.

## Aggressive Retry Strategy (Opt-In)

**Pros**&#x20;

- Retries against a broader set of decline codes, which will attempt transactions the default model will not attempt.
- Recovers an additional 2% of invoices that the default strategy may not be able to get.  This is useful for merchants whose priority is maximizing churn reduction over the risks below.

**Cons**

- Risks breaching card-network retry-limit mandates, which can result in per-transaction fines or a merchant being placed on monitoring or remediation plans with an acquirer.
- Higher risk of transaction patterns being flagged as adversarial or fraud-like behavior.
- Risks customer experience if retries are perceived as excessive.  Some customers are notified of declined transactions through their card apps.  This presents an even greater challenge if customers are notified by the merchant at the time of each attempt. &#x20;

<br />

<br />
