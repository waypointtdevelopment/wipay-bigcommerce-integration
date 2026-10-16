# Waypoint WiPay for BigCommerce

An independent BigCommerce integration research project maintained by Waypoint. It is not affiliated with, sponsored by, or endorsed by WiPay.

## Project status

**Feasibility research only.** No Waypoint-supported BigCommerce payment gateway is available. BigCommerce's documented Payments API does not support hosted/offsite providers, while WiPay's current API uses hosted checkout. A provider-partner route must be confirmed before implementation.

## What you can actually do with WiPay on BigCommerce today

There is no native WiPay gateway you can install from this repository. If a BigCommerce merchant still wants to use WiPay, the realistic path is a manually reconciled workflow: create the order through a BigCommerce offline/manual payment method, start the WiPay hosted checkout from a separate backend or test app using the exact order amount, verify the WiPay result server-side, and then reconcile and update the BigCommerce order by hand.

This project includes a [workaround guide](GUIDE.md) that walks through that sandbox workflow, including the request, verification, and reconciliation steps. It is a test and reconciliation guide, not a production gateway and not an automated BigCommerce integration.

## Research

See [PLATFORM-RESEARCH.md](PLATFORM-RESEARCH.md) for the hard constraint, the offline-payment and Transactions-API realities, the provider-list open point, and official references.

## Ownership and disclaimer

Waypoint maintains this independent research project. WiPay does not endorse it. Use is at your own risk; no warranty is provided.
