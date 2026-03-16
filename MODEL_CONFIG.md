# AI Model Configuration

Distinct reads AI model selection from a JSON object with this exact top-level structure:

```json
{
  "genai": {
    "chatAgent": "your-model-name",
    "learnAgent": "your-model-name",
    "exploreAgent": "your-model-name",
    "validationAgent": "your-model-name",
    "namingChat": "your-model-name",
    "indexationOverview": "your-model-name",
    "indexationGeneral": "your-model-name",
    "indexationDescription": "your-model-name",
    "contextChooseTables": "your-model-name",
    "contextIdentifyTables": "your-model-name",
    "contextSummarise": "your-model-name",
    "queryGenerator": "your-model-name",
    "getChatInsights": "your-model-name",
    "selfHealing": "your-model-name",
    "dataTabQuery": "your-model-name",
    "dataView": "your-model-name",
    "connectionTest": "your-model-name",
    "embedding": "your-model-name"
  },
  "vertex": {
    "chatAgent": "your-model-name",
    "learnAgent": "your-model-name",
    "exploreAgent": "your-model-name",
    "validationAgent": "your-model-name",
    "namingChat": "your-model-name",
    "indexationOverview": "your-model-name",
    "indexationGeneral": "your-model-name",
    "indexationDescription": "your-model-name",
    "contextChooseTables": "your-model-name",
    "contextIdentifyTables": "your-model-name",
    "contextSummarise": "your-model-name",
    "queryGenerator": "your-model-name",
    "getChatInsights": "your-model-name",
    "selfHealing": "your-model-name",
    "dataTabQuery": "your-model-name",
    "dataView": "your-model-name",
    "connectionTest": "your-model-name",
    "embedding": "your-model-name"
  }
}
```

## Rules

- `genai` is used when `distinct.ai.provider` is `genai`.
- `vertex` is used when `distinct.ai.provider` is `vertex`.
- Every value must be a non-empty string.
- Distinct does not validate model names against a built-in list.
- Distinct does not fall back to another provider.
- If the active provider is missing, or any required key is missing for that provider, the request fails.

## Key Descriptions

- `learnAgent`: Model used for Learn mode (researching and formalizing data warehouse knowledge). Can differ from `chatAgent` if you want a lighter or different model for learn tasks.
- `connectionTest`: Model used when the user tests their AI connection (e.g. in Settings). Use a lightweight model like `gemini-2.0-flash-lite`.
- `embedding`: Model used for vector embeddings (LanceDB, semantic search). Must output 768 dimensions (e.g. `gemini-embedding-001`).
- `reviewEnrichment`: Model used by the **web app** when enriching a review request (annotating SQL and generating analysis summary). Falls back to `chatAgent` if missing.

## Firebase Remote Config

Create a Firebase Remote Config parameter named `model_config`.

Set its value to the full JSON object shown above.

Example:

```json
{
  "genai": {
    "chatAgent": "gemini-2.5-pro",
    "learnAgent": "gemini-2.5-pro",
    "exploreAgent": "gemini-2.5-pro",
    "validationAgent": "gemini-2.5-pro",
    "namingChat": "gemini-2.5-flash-lite",
    "indexationOverview": "gemini-2.5-flash",
    "indexationGeneral": "gemini-2.5-flash",
    "indexationDescription": "gemini-2.5-flash-lite",
    "contextChooseTables": "gemini-2.5-flash-lite",
    "contextIdentifyTables": "gemini-2.5-flash-lite",
    "contextSummarise": "gemini-2.5-flash",
    "queryGenerator": "gemini-2.5-flash",
    "getChatInsights": "gemini-2.5-flash",
    "selfHealing": "gemini-2.5-flash",
    "dataTabQuery": "gemini-2.5-flash-lite",
    "dataView": "gemini-2.5-flash-lite",
    "connectionTest": "gemini-2.0-flash-lite",
    "embedding": "gemini-embedding-001"
  },
  "vertex": {
    "chatAgent": "gemini-2.5-pro",
    "learnAgent": "gemini-2.5-pro",
    "exploreAgent": "gemini-2.5-pro",
    "validationAgent": "gemini-2.5-pro",
    "namingChat": "gemini-2.5-flash-lite",
    "indexationOverview": "gemini-2.5-flash",
    "indexationGeneral": "gemini-2.5-flash",
    "indexationDescription": "gemini-2.5-flash-lite",
    "contextChooseTables": "gemini-2.5-flash-lite",
    "contextIdentifyTables": "gemini-2.5-flash-lite",
    "contextSummarise": "gemini-2.5-flash",
    "queryGenerator": "gemini-2.5-flash",
    "getChatInsights": "gemini-2.5-flash",
    "selfHealing": "gemini-2.5-flash",
    "dataTabQuery": "gemini-2.5-flash-lite",
    "dataView": "gemini-2.5-flash-lite",
    "connectionTest": "gemini-2.0-flash-lite",
    "embedding": "gemini-embedding-001"
  }
}
```

## Local Override File

For advanced users, a JSON file can be stored locally at:

```text
<extension-global-storage>/model_config.json
```

The local file is **merged over** the remote config. You can override a subset of models—only include the keys you want to change. Keys not in the local file are inherited from the remote config.

Example: override only `chatAgent` and `learnAgent` for genai:

```json
{
  "genai": {
    "chatAgent": "gemini-2.0-flash",
    "learnAgent": "gemini-2.0-flash"
  }
}
```

The remote config supplies all other keys. If there is no remote config, the local file must define all required keys for your provider.

### Where is extension-global-storage?

`<extension-global-storage>` is the VS Code/Cursor extension global storage directory. The extension uses `context.globalStorageUri.fsPath` (see `modelConfigService.ts`). The path depends on your OS and editor:

| OS      | VS Code path                                                                 | Cursor path                                                                 |
|---------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| macOS   | `~/Library/Application Support/Code/User/globalStorage/Mangabey.distinct/`   | `~/Library/Application Support/Cursor/User/globalStorage/Mangabey.distinct/` |
| Windows | `%APPDATA%\Code\User\globalStorage\Mangabey.distinct\`                       | `%APPDATA%\Cursor\User\globalStorage\Mangabey.distinct\`                   |
| Linux   | `~/.config/Code/User/globalStorage/Mangabey.distinct/`                       | `~/.config/Cursor/User/globalStorage/Mangabey.distinct/`                    |

**How to find it from the editor:** Command Palette → **Developer: Open User Data Folder**, then navigate to `User/globalStorage/Mangabey.distinct/`. The full path to the override file is `.../globalStorage/Mangabey.distinct/model_config.json`.

## Web Backend (Python)

The web backend (Knowledge API) reads from Firebase Remote Config for:

- `genai.reviewEnrichment` — review request enrichment (annotated SQL, analysis summary)

Falls back to `genai.chatAgent` if the key is missing, then to a hardcoded default (`gemini-3-pro-preview`).

**Requirements:** Set `FIREBASE_APP_ID` in the backend environment (or `.env`). Use the same value as the VS Code extension. The backend also needs `FIREBASE_PROJECT_ID` and `FIREBASE_API_KEY`. When `FIREBASE_APP_ID` is unset, the backend skips the fetch and uses hardcoded defaults.

**How to update the remote config:** See [Firebase Remote Config](#firebase-remote-config) above. Add `reviewEnrichment` under `genai` in the `model_config` parameter. Example:

```json
{
  "genai": {
    "chatAgent": "gemini-2.5-pro",
    "reviewEnrichment": "gemini-2.5-flash",
    ...
  }
}
```
