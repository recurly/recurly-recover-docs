---
title: Multi-payment method, single gateway
excerpt: >-
  Create recovery invoices via API and learn best practices around testing
  against multiple payment methods, and single gateway setup.
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
# Overview

This guide will cover the testing best practices for using multiple payment methods on a single gateway.

If you are using gateway tokens, ensure the gateway you have enabled has access to those tokens -- this is necessary for a successful implementation.

### Prerequisites & limitations

- Ensure you have reviewed the basic API Guide and are familiar with the fields in the Recovery endpoint.
- You have enabled a single gateway in your Recurly sandbox site.
- If you are using gateway tokens, you have confirmed that the tokens in use are accessible via your enabled gateway. Example, if you provide Recurly with Braintree gateway tokens, the enabled Braintree gateway must have access to them.
- If your gateway tokens require NTID reference, you have the NTIDs available for Recurly to store and send.

***

# Definition

Text

***

## Best Practices&#x20;

* A&#x20;
* B
* C

## Integration Guide

### Example using Multiple Payment Methods (Tokens) and Single Gateway

```json
```

###
