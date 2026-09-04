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
* **Keep backup methods current&#x20;**— expired backups provide no real coverage. When a customer adds a new payment method to your company's wallet system, ensure you are providing that detail to Recurly.
* **Be transparent that a backup method may be charged if the primary fails**, so it isn't a surprise to the customer.
* **Let the customer designate a preferred backup** vs. setting the backup arbitrarily — some customers want control over which method absorbs a failed charge
