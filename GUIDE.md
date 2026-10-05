# WiPay Payments API workaround guide for BigCommerce

**Project type:** documentation and sandbox test guide. This is not a BigCommerce payment plugin and does not add WiPay to native BigCommerce checkout.

## Platform limitation

BigCommerce's public Payments API does not support hosted or offsite payment providers, and its Checkout SDK cannot add new payment methods. WiPay's Payments API redirects the buyer to WiPay's hosted checkout, so it cannot be represented as a native BigCommerce gateway through those APIs.

## Workaround scope

This guide describes a manually reconciled sandbox workflow, not a production-ready gateway:

- Where the store offers an offline/manual checkout method, use it only to create a pending test order. The method name and instructions should tell buyers that payment is handled separately and the order is not paid yet.
- A separate merchant-controlled backend or test app can create a WiPay hosted-checkout request using the BigCommerce order reference and exact order amount.
- After WiPay returns the customer, verify the result on that backend. A merchant must reconcile the verified transaction with the BigCommerce order and update its status manually.
- Do not collect card details in BigCommerce custom fields, checkout scripts, or storefront code. Do not treat an unverified redirect as proof of payment.

This does not sync WiPay payment status into BigCommerce. It can also affect inventory reservation and customer expectations, so merchants should review their order-status and fulfillment workflow before use. BigCommerce B2B invoice/offline-payment APIs are a separate workflow and are not covered here.

## Sandbox walkthrough

1. Use a test BigCommerce store. Confirm that an offline/manual payment option is available in its checkout. Do not use the BigCommerce Payments API to try to process WiPay hosted checkout.
2. Place a test order using that offline option. Record its order ID, expected total, and currency. Treat the order as unpaid.
3. From a separate backend or WiPay's official API collection, POST a WiPay Payments API request to the sandbox endpoint for the merchant's territory. For Trinidad and Tobago, this is https://ttsb.wipayfinancial.com/plugins/payments/request.
4. Set environment to sandbox, account number to 1234567890, and include the territory, currency, credit-card method, fee structure, unique order_id, origin, original total, and test-backend response_url. Follow WiPay's current [Payment Request reference](https://docs.wipayfinancial.com/payments-api) and [sandbox environment table](https://docs.wipayfinancial.com/platforms-and-environments).
5. Complete one approved and one declined transaction using the test-card numbers from WiPay's current testing documentation.
6. On the server, verify every successful response hash using the sandbox API key 123 and the original amount sent in the request. Compare transaction ID, order_id, amount, and currency with the stored test order.
7. Only after verification, manually reconcile and update the BigCommerce test order. Keep declined, cancelled, mismatched, or unverified attempts unpaid.

## Security and test boundaries

- The API key is for server-side response-hash verification only. Never place it in storefront JavaScript, theme files, page source, or a public repository.
- Keep all requests on WiPay sandbox hosts and use sandbox identifiers only. Never substitute live credentials or endpoints during this exercise.
- Use a unique order_id per payment attempt and prevent duplicate reconciliation.
- This workflow has no automatic BigCommerce order-state callback, transaction ledger entry, refund handling, or production support promise.

## Official references

- [WiPay Payments API](https://docs.wipayfinancial.com/payments-api)
- [WiPay sandbox environments](https://docs.wipayfinancial.com/platforms-and-environments)
- [WiPay API collections](https://docs.wipayfinancial.com/api-collections)
- [WiPay getting started and response verification](https://docs.wipayfinancial.com/getting-started)
- [BigCommerce Payments API limitations](https://docs.bigcommerce.com/developer/docs/admin/checkout-and-cart/payments/overview)
- [BigCommerce checkout customization limits](https://docs.bigcommerce.com/developer/docs/admin/checkout-and-cart)
- [BigCommerce payment method reference](https://docs.bigcommerce.com/developer/api-reference/rest/admin/payments/methods/v2/get-all-payment-methods)
