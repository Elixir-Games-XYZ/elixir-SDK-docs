---
description: node.js example of RSA signature
---

# 🔢 Node.js Example

```javascript
const { createSign, createVerify } = require('crypto')
/** *
* @param {string} privateKey
* @param {number} token
* @param {string | object} data
* @returns 
*/
function signRSARequest ( 
   privateKey,
   token = Date.now(), 
   data = {}
){
   const info = JSON.stringify(data) 
try {
   const signer = createSign('rsa-sha256' ) 
   signer.update(`${info}.${token}`)
   return signer.sign(privateKey, 'hex')

 } catch (err) {
   throw new Error(`Could not perform signature: ${err.message}`)
}
```
