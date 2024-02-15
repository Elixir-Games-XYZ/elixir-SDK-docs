---
description: Submit the user progress to advance in the Quest
---

# Update Progress

Finally, the Progress Reporting Endpoint enables game servers to securely report user progress events to the Quest System API. This server-to-server communication ensures the integrity and authenticity of progress reports through RSA signature-based authentication.

#### Authentication Workflow:

1. **API Key Generation:**
   * Game developers will need to get their [key pairs](../../management/api-keys.md) consisting of public and private keys.
   * Private keys are securely stored on the game server and used to sign progress reports.
2. **RSA Signature Generation:**
   * Before sending a progress report, the game server generates an RSA signature for the request payload using its private key.
   * The signature is appended to the request headers for authentication purposes.
3. **Signature Verification:**
   * Upon receiving a progress report, the Quest System API server extracts the RSA signature from the request headers.
   * The API server validates the signature against the corresponding public key associated with the game server.
   * If the signature is valid, the progress report is accepted and processed. Otherwise, the request is rejected.

{% content-ref url="../../../api-docs/api-docs-1/game-quests.md" %}
[game-quests.md](../../../api-docs/api-docs-1/game-quests.md)
{% endcontent-ref %}

The Progress Reporting Endpoint facilitates secure and reliable communication between game servers and the Quest System API, ensuring the integrity and authenticity of progress reports through RSA signature-based authentication. By following the authentication workflow and adhering to the request format, game developers can seamlessly integrate progress reporting into their server-side systems, enabling users to advance in quests and earn rewards effectively.

\
