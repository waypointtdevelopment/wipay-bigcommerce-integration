# Platform research: BigCommerce

## Status
Feasibility workspace only. BigCommerce's documented Payments API does not support hosted/offsite providers, while WiPay's current Payments API is a hosted-checkout redirect.

## Implication
A direct integration through that Payments API is not an evident fit. A provider-partner route may require BigCommerce/WiPay onboarding and a different design. Defer implementation until WiPay confirms the path for its territories.

## Next decisions
- Ask if WiPay can onboard as an approved/open BigCommerce payment provider.
- Confirm permitted checkout flow, territories, existing package/support, and operational expectations.

## References
- [BigCommerce Payments API](https://docs.bigcommerce.com/developer/docs/admin/checkout-and-cart/payments/overview)
- [WiPay Payments API](https://docs.wipayfinancial.com/payments-api)
- [WiPay Plugin Integration Guides](https://wipaycaribbean.com/solutions/plugins)
