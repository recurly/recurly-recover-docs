---
title: Retry Strategy Models
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

&#x20;

<br />

<br />
