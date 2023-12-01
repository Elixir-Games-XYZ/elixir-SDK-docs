# Developer

Utilize our API to access product details, seamlessly integrate in-app purchases within your game, effectively administer content access, and securely receive transaction information signed by Elixir Store. This documentation provides guidance on implementing these features for a streamlined integration process.

{% hint style="danger" %}
**The integration and utilization of the Elixir SDK Auth constitute mandatory prerequisites for engaging with the In-App Purchases system.** Eligibility for leveraging the In-App Purchases system is contingent upon the association of Elixir accounts with respective internal accounts.
{% endhint %}

## 1. Configure your Store

[Create your in-app purchases store](./#1.-configure-your-store) effortlessly by adding metadata, including product name, description, price, and currency, and submit it for review. [Submit your products](submit-product.md) for review following our [review guidelines](../review-guidelines.md).\
\
Additionally, generate essential [in-app purchase keys](client-integration.md) to facilitate the processing of Elixir Store-signed transactions. This documentation guides you through the steps required for a seamless implementation.

## 2. Implement Elixir SDK

Incorporate in-app purchase capability seamlessly into your [Unity](../../../sdk/unity/elixir-overlay.md) or [Unreal](../../../sdk/unreal-engine.md) game. Our testing environment within the editor enables you to replicate overlay events, facilitating in-app purchase testing without incurring charges through test accounts. Validate your implementation by thoroughly testing each aspect of your code using your game to initiate in-app purchases.

For additional testing, explore your game and in-app purchases on the internal [Develop branch](../../management/version-control.md).&#x20;

## 3. Handle post-payment event

Receive the purchase status and validation in your backend system. Check the Elixir Store signature and appropriately allocate the items to the respective players. This [documentation](handle-post-payments.md) provides instructions on seamlessly implementing these backend processes for efficient handling of in-app purchases.





