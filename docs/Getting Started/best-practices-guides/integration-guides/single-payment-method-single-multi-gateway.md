---
title: Single payment method, single or multiple gateways
excerpt: >-
  Create recovery invoices via API and learn best practices around testing
  against a single payment method, and single or multi-gateway setup.
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
# Overview

This guide will cover the testing best practices for both the single/single and single/multiple (payment method&#x20;

Generally, the Single method / Single gateway is the easiest to implement and test in your recovery suite. If you are using gateway tokens, multiple gateways and token to gateway_code hygiene is necessary for a successful implementation.

### Prerequisites & limitations

- Ensure you have reviewed the basic API Guide and are familiar with the fields in the Recovery endpoint.
- You have enabled one or more gateways in your Recurly sandbox site.
- If you are using gateway tokens, you have awareness of which tokens are accessible via your enabled gateways. Example, if you provide Recurly with Braintree gateway tokens, the enabled Braintree gateway must have access to them.
- If your gateway tokens require NTID reference, you have the NTIDs available for Recurly to store and send.

***

# Definition

**Creating Recovery Invoices** refers to the process of generating a new invoice via the Recurly API specifically to retry collection on a failed or past-due subscription charge, without disrupting the original billing cycle or subscription state. This guide specifically covers using a single payment method with a single or multi-gateway setup.

***

## Best Practices&#x20;

* A&#x20;
* B
* C

## Integration Guide

### Example using Single Payment Method (Token) and Single Gateway

```json
```

### Example using Single Payment Method (Token) and Multi Gateway

```json
```

###
