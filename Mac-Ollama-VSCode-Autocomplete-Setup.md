### 1. Install Continue

Open VS Code, navigate to the Extensions Marketplace (`Cmd + Shift + X`), search for **Continue**, and install it.

### 2. Pull Models & Run Ollama in Debug Mode

1. Quit the Ollama UI App from your macOS menu bar.
2. Download both the autocomplete and chat models:

```bash
ollama pull codegemma:2b
ollama pull codegemma:7b

```

3. Restart Ollama in verbose debug mode:

```bash
OLLAMA_DEBUG=1 ollama serve

```

### 3. Update VS Code Global User Settings

Open global **User Settings (JSON)** (`Cmd + Shift + P` ➡️ *Preferences: Open User Settings (JSON)*) and apply these keys:

```json
{
    "chat.disableAIFeatures": false,
    "editor.tabCompletion": "on",
    "editor.inlineSuggest.enabled": true,
    "continue.enableTabAutocomplete": true,
    "continue.enableNextEdit": false
}

```

### 4. Configure `.continue/config.yaml`

Open `~/.continue/config.yaml` and map the models using Continue's role-based schema format:

```yaml
name: Local Config
version: 1.0.0
schema: v1

models:
  - name: CodeGemma Chat (7B)
    provider: ollama
    model: codegemma:7b
    roles: [chat, edit, apply]

  - name: CodeGemma Auto (2B)
    provider: ollama
    model: codegemma:2b
    roles: [autocomplete]

```

### 5. Verification

* Open a source file and begin typing.
* The `2b` model handles quick inline autocompletions (press `Tab` to accept ghost text) throwing a `POST /api/generate` log entry in your terminal.
* Highlighting code and hitting `Cmd + L` or `Cmd + I` routes complex reasoning, refactoring, and code edits to the smarter `7b` model.
