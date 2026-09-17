# vscode-copilot-custom-endpoint-settings
Based on the VS Code docs, here's the full set of model-level options you can add to a custom endpoint entry in `chatLanguageModels.json`:

| Property | Description |
|---|---|
| `id` | Model identifier sent to the API |
| `name` | Display name in the model picker |
| `url` | Full endpoint URL |
| `apiType` | Per-model override: `chat-completions`, `responses`, or `messages` |
| `toolCalling` | `true` if the model supports tool calling (required for the model to appear in the picker) |
| `vision` | `true` if the model supports **image** inputs |
| `maxInputTokens` / `maxOutputTokens` | Token limits (input + output must fit within the models context so look them up) |
| `contextWindow` | Full context window (input + output); lets you omit `maxInputTokens` |
| `editTools` | Array: `find-replace`, `multi-find-replace`, `apply-patch`, `code-rewrite` |
| `thinking` | `true` if the model has thinking/reasoning capabilities |
| `streaming` | `true` if streaming is supported (default `true`) |
| `zeroDataRetentionEnabled` | `true` to enable ZDR (affects `previous_response_id` behavior) |
| `supportsReasoningEffort` | Array of effort levels, e.g. `["low", "high", "max"]` (look up the levels your model supports) |
| `reasoningEffortFormat` | `chat-completions`, `responses`, or `messages` — controls body shape |
| `modelOptions` | Arbitrary request params, e.g. `{"temperature": 0.2, "top_p": 0.9}` |
| `requestHeaders` | Extra HTTP headers for the request |

**On video and audio:** There is **no** `audio` or `video` option in the current configuration. The only non-text modality flag is `vision` (image input). VS Code's chat input doesn't currently support attaching or sending video/audio content to models, so even if your endpoint could accept them, there's no way to declare or use that capability through the custom endpoint config. You're limited to text + images (via `vision: true`).

Example kodekloud kodekey
```
[
	{
		"name": "KodeKloud AI",
		"vendor": "customendpoint",
		"apiKey": "lmao",
		"apiType": "chat-completions",
		"models": [
			{
				"id": "zai/glm-5.3-flash",
				"name": "GLM 5.3 Flash",
				"url": "https://api.ai.kodekloud.com/v1/chat/completions",
				"toolCalling": true,
				"vision": true,
				"supportsReasoningEffort": [
					"low",
					"high",
					"max"
				],
				"contextWindow": 1040000,
				"maxOutputTokens": 128000
			}
		],
		"settings": {
			"zai/glm-5.3-flash": {
				"reasoningEffort": "max"
			}
		}
	}
]
```
