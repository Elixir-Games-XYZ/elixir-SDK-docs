# Handle Post-Payments

## Store API Keys

Generating an in-app purchase key enables Elixir to authenticate and validate requests between the client and server or server-to-server, specifically about in-app purchases. This includes authentication for Elixir Store server webhooks designed for post-payment events.

### Modify your server webhook

1. Go to your Game API Keys section
2. Scroll to the In-App Purchases Key
3. Click on the "Edit" button and modify the input

<figure><img src="../../../.gitbook/assets/Frame 284.png" alt=""><figcaption></figcaption></figure>

## Post-payment & Signature

To secure the server-to-server communication for in-app purchase post-payment events, we employ an RSA signature process. The client possesses the capability to validate the signed webhook received from the Elixir Store server using their public key.
