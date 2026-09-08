---
title: Multiple Payment Methods
deprecated: false
hidden: true
metadata:
  robots: index
---
## Overview

Recurly Recover enables your site with Recurly Wallet by default, giving you the option of adding one or many payment methods on a recover invoice. Customers with a single card or payment method on file are vulnerable to any decline — expired or reissued cards, or temporary holds all interrupt an invoice's recovery rate. See our best practices below to improve your recovery rates across the board.&#x20;

### Best Practices

* **Encourage customers to add a second payment method proactively** (at signup or account settings), not just after a failed charge. When sending recovery invoices to Recurly, you can include both methods so Recurly can retry against any applicable method the customer has provided.
* **Favor variety (mix payment methods) over a duplicate** — the ApplePay derivative of the same PAN offers little protection. Instead, preferring a different card network or a PayPal option is more resilient.
* **Keep backup methods current&#x20;**— expired backups provide no real coverage. When a customer adds a new payment method to your company's wallet system, ensure you are providing that detail to Recurly. You may also periodically nudge customers to keep their payment methods current (recommend deleting expired cards from their wallet).
* **Be transparent that a backup method may be charged if the primary fails**, so it isn't a surprise to the customer.
* **Let the customer designate a preferred backup** vs. setting the backup arbitrarily — some customers want control over which method absorbs a failed charge

### Ensure Success

To ensure you are set up for success with multiple payment methods, ensure you have the following available:&#x20;

* **If you are using raw card data**, ensure you have the primary (and backup) payment method data for your customers including: **PAN** (the full 15-16 digit card number), **Expiration Date**, and the **NTID** (Network Transaction ID / Scheme ID) for the specific invoice you are recovering. These PANs will likely have different NTIDs, especially if they are different card numbers.
* **If you are using gateway tokens**, ensure you have the gateway token that represents each payment method for the consumer. Depending on the gateway, you may also need to provide the expiration date and NTID you keep on file for the customer's subscription. Exceptions are: Stripe, Braintree, PayPal Complete.
* **Enable Token Backfilling** -- if you don't have the meta-data available for your tokens, we can query your gateway to get up to date information about the card brand, up to date expiration date if required by the gateway for processing. You will need to enable certain permissions at the gateway level in certain cases to allow this query to be successful.

Additionally, some tips and best practices are available within the specific API guides and Testing guidelines for these specific use cases:

- [Multiple Payment Methods, Single Gateway](https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/multi-payment-method-single-gateway)
- [Multiple Payment Methods, Multiple Gateways](https://docs.recurly.com/recurly-recover/v1.0_retry-agent-best-practices-guides/docs/multi-payment-method-multi-gateway)

Depending on which use case you fall under, follow the guidelines and ensure you’ve got the right setup in your Recurly site to support your recovery efforts. By default, all Recurly Recover sites are set up with Recurly Wallet, allowing multiple payment methods to be used if you have them available for your customers.
