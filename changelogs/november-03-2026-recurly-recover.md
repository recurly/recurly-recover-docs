---
title: November 03, 2026 - Recurly Recover
author: Jenn Schnoes
hidden: true
published_at: '2026-11-02T21:32:23.636Z'
---
This release expands Recurly’s Recovery gateway onboarding capabilities significantly, with Adyen, FreedomPay, and Commerce Hub (Fiserv) now all available to onboard directly through the Recovery gateway interface, making it easier for merchants to configure additional gateways for retry and recovery workflows without additional setup friction.

The Recovery endpoint also gains two new API enhancements: merchants using Adyen can now explicitly specify a shopper reference for Adyen gateway tokens, and merchants who do not use or require gateway tokens can now send a full PAN and expiry date directly to the Recovery endpoint — provided the NTID is explicitly included in the request. See updated V3 API documentation after release for implementation details.

| Release Date | Feature                    | Type        | Potential Impact | Description / Overview                                                                                                                                        |
| ------------ | -------------------------- | ----------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nov 03       | Adyen Gateway              | Enhancement | Low              | Merchants can now onboard Adyen gateway through the Recovery gateway onboarding interface.                                                                    |
| Nov 03       | FreedomPay Gateway         | Enhancement | Low              | Merchants can now onboard FreedomPay gateway through the Recovery gateway onboarding interface.                                                               |
| Nov 03       | Commerce Hub Gateway       | Enhancement | Low              | Merchants can now onboard Commerce Hub (Fiserv) gateway through the Recovery gateway onboarding interface.                                                    |
| Nov 03       | V3 API - Recovery Endpoint | Enhancement | Medium           | Merchants can now specify an Adyen gateway token's shopper reference explicitly via API.                                                                      |
| Nov 03       | V3 API - Recovery Endpoint | Enhancement | Low              | Merchants can now send full PAN and expiry date to the Recovery endpoint if they do not have or require gateway tokens. Requires sending the NTID explicitly. |
| Nov 3        | Recover: full PAN          | Enhancement | Low              | Accepting full PAN in Recover offers more options for customers.                                                                                              |