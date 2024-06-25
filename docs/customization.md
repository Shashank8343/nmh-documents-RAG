# Customizing the Chat App

This guide provides more details for customizing the Chat App.

#### Making settings overrides permanent

The UI provides a "Developer Settings" menu for customizing the approaches, like disabling semantic ranker or using vector search.
Those settings are passed in the "context" field of the request to the backend, and are not saved permanently.
However, if you find a setting that you do want to make permanent, there are two approaches:

1. Change the defaults in the frontend. You'll find the defaults in `Chat.tsx` and `Ask.tsx`. For example, this line of code sets the default retrieval mode to Hybrid:

```typescript
const [retrievalMode, setRetrievalMode] = useState<RetrievalMode>(RetrievalMode.Hybrid);
```

You can change the default to Text by changing the code to:

```typescript
const [retrievalMode, setRetrievalMode] = useState<RetrievalMode>(RetrievalMode.Text);
```

2. Change the overrides in the backend. Each of the approaches has a `run` method that takes a `context` parameter, and the first line of code extracts the overrides from that `context`. That's where you can override any of the settings. For example, to change the retrieval mode to text:

```python
overrides = context.get("overrides", {})
overrides["retrieval_mode"] = "text"
```

By changing the setting on the backend, you can safely remove the Developer Settings UI from the frontend, if you don't wish to expose that to your users.

