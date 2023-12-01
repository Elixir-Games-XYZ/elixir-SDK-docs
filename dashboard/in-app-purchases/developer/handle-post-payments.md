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

### Elixir Store Server Response

```json
// 
{
  "order": {                                             // List of products purchased in the order
    "products": [
      {
        "_id": "65413fd1bb194c67b621c1ca",
        "sku": "candies-250",                            // SKU of the product
        "name": "250 Candies (Tinies)",
        "description": "",
        "imageUrl": "example",                           // Product image URL
        "status": "ACTIVE",                              // Product status
        "category": "IN_APP",                            // Product category
        "disabled": false,                               // Product is enabled
        "clientId": "tinies",                            // Client ID
        "createdAt": "2023-10-31T17:56:33.410Z",
        "updatedAt": "2023-10-31T17:56:33.410Z",
        "price": 50,                                     // Total price (considering quantity and discount)
        "baseCurrency": null,                            // Base currency used in case of a conversion (set to null if there was no conversion)
        "id": "65413fd1bb194c67b621c1ca",                // Product ID
        "quantity": 2,                                   // Quantity of the product purchased
        "unitBasePrice": 25,                             // Price of the product in unit
        "discount": 0                                    // Product discount
      }
    ],
    "userId": "6a431244-4658-4532-8a06-178e41fff0e7",    // ID of the user that did the purchase
    "totalPrice": 50,                                    // Total price of the order
    "currency": "USD",                                   // Currency of the order
    "rate": 1,                                           // Rate used in case there was a conversion of currency
    "usdAmount": 50,                                     // Total price in USD
    "usdExchangeRate": 1                                 // USD exchange rate
  },
  "signature": "0cbdec9f50e1cd4..."
}
```

### Signature Code Sample

```javascript
import { createPublicKey, createVerify } from 'crypto'

// Where message its a JSON.stringify from the order object
function verifySignature(signature: string, message: string): boolean {
  const publicKey = createPublicKey({
    key: Buffer.from(
      process.env['GAME_PUBLIC_KEY'] as string,
      'hex'
    ),
    type: 'spki',
    format: 'der',
  })
  const verifier = createVerify('rsa-sha256')
  verifier.update(message)
  verifier.end()
  const isVerified = verifier.verify(publicKey, signature, 'hex')
  return isVerified
}

export { verifySignature }
```
