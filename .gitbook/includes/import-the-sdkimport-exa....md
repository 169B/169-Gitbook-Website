---
title: // Import the SDKimport Exa...
---

{% code title="index.js" overflow="wrap" %}
```javascript
// Import the SDK
import ExampleAPI from "example-api";

// Initialize the client
const client = new ExampleAPI({ apiKey: "YOUR_API_KEY" });

// Send your first message
const response = await client.messages.send({
  message: "Hello, world!"
});

```
{% endcode %}
