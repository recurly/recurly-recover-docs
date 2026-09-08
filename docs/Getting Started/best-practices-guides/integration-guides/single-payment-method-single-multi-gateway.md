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

Text

***

## Best Practices&#x20;

<br />

## Integration Guide

### Step 1: Generate a Recovery Invoice&#x20;

```text
```

### Step 2: Listen to Webhooks&#x20;

<br />

### Step 3: Manage External Payment Method Lifecycle

###
