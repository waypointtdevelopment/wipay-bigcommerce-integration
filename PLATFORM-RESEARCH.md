# Platform research: BigCommerce

## Status
Feasibility workspace only. BigCommerce's documented Payments API does not support hosted/offsite providers, while WiPay's current Payments API is a hosted-checkout redirect.

## Implication
A direct integration through that Payments API is not an evident fit. A provider-partner route may require BigCommerce/WiPay onboarding and a different design. Defer implementation until WiPay confirms the path for its territories.

## What is buildable today
BigCommerce supports merchant-configured offline/manual payment methods such as bank deposit, cash on delivery, check, money order, and pay in store, and orders can remain **Awaiting Payment** until payment is confirmed. That is the most realistic merchant-facing manual-reconciliation path if no native provider exists. BigCommerce also documents a Transactions API that can record externally processed payments, but its current provider list is Adyen, Authorize.net, BigCommerce Payments, Braintree, PayPal Commerce Platform, and Stripe; WiPay is not listed, so it is not an open generic external-transaction route.

- [Offline payment methods](https://support.bigcommerce.com/s/article/Offline-Payment-Methods?language=en_US)
- [Order statuses](https://docs.bigcommerce.com/developer/api-reference/rest/admin/management/orders/order-status/get-order-statuses)
- [Transactions API](https://docs.bigcommerce.com/developer/docs/admin/checkout-and-cart/payments/transactions-api)
- [Update Order](https://docs.bigcommerce.com/developer/api-reference/rest/admin/management/orders/update-order)

## Hard constraint
BigCommerce's Payments API processes payments through the store's connected gateways and explicitly says its API flow does not support hosted or offsite providers. The Checkout SDK cannot add new payment methods. Because WiPay's current API redirects the buyer to a hosted checkout, it cannot be represented as a native BigCommerce gateway through those APIs.

## What is not buildable today
There is no documented generic Payments API route to add WiPay as a hosted redirect payment method. Update Order can change order fields and status, but that should not be confused with a supported payment transaction or processor integration.

## Next decisions
- Ask BigCommerce whether WiPay can onboard as an approved/open payment provider, and confirm the permitted checkout flow, territories, existing package/support, and operational expectations.
- Confirm whether BigCommerce adds WiPay to the Transactions API provider list, because that is the only public path that comes close to recording externally processed payments.

## References
- [BigCommerce Payments API](https://docs.bigcommerce.com/developer/docs/admin/checkout-and-cart/payments/overview)
- [WiPay Payments API](https://docs.wipayfinancial.com/payments-api)
- [WiPay Plugin Integration Guides](https://wipaycaribbean.com/solutions/plugins)
