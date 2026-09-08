---
title: Integration and testing
excerpt: Review testing best practices and integration guides for your unique use case.
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
# Overview&#x20;

In general, you'll want to follow our standard Go-live checklist like any Recurly merchant, but since you are leveraging our Retry strategies, there are specific testing behaviors you should employ before going live.

## Best Practices&#x20;

* Start with **a small percentage of your overall volume** to ensure your live traffic is flowing properly
* **Increase your volume over a period of time&#x20;**(of your choice), but let data drive your moves
* You can **create multiple Dunning campaigns** to create cohorts and traffic your success rates among statistically unique customer groups of your choice
* **Experiment with different dunning campaign durations&#x20;**&#x74;o see if extending your retry timeframe helps capture long-tail returns.
* **Customize your testing behavior** based on your own specific payment method + gateway combination. One or more use cases may be applicable to you depending on your customer dataset and the gateways you choose to enable.

## Use-Case Driven Testing and Integration Guides

* Single Payment Method, Single Gateway
* Multi-Payment Method, Single Gateway
* Multi-Payment Method, Multi-Gateway

#
