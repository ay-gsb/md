### 1. Install DevoxxGenie

Open IntelliJ IDEA (requires **version 2024.3 or later** for native inline ghost-text rendering), go to **Settings** (`Cmd + ,`) ➡️ **Plugins** ➡️ **Marketplace**, search for **DevoxxGenie**, and install it.

### 2. Pull Models

1. Quit the Ollama UI App from your macOS menu bar.
2. Download both the autocomplete and chat models:

```bash
ollama pull codegemma:2b
ollama pull qwen2.5-coder:7b

```

3. Restart Ollama in verbose debug mode:

```bash
OLLAMA_DEBUG=1 ollama serve

```

### 3. Configure IntelliJ Global & Core Settings

Ensure IntelliJ allows third-party plugins to stream ghost text without interference from native code completion fragments:

1. Open IntelliJ **Settings** (Cmd + ,) ➡️ **Editor** ➡️ **General** ➡️ **Code Completion**.
2. Uncheck **"Show suggestions as you type"** if you want DevoxxGenie to handle 100% of your ghost text exclusively, or keep it on to let them mix.


### 4. Configure DevoxxGenie Providers & Models

DevoxxGenie isolates inline Fill-in-the-Middle (FIM) autocomplete from chat settings.

* **Set Up Chat Logic (qwen2.5-coder):**
  1. Open the **DevoxxGenie** tool window panel on the right side of the IDE.
  2. Set **LLM Provider** to `Ollama`.
  3. Click **Refresh Models** and select `qwen2.5-coder:7b` from the model dropdown.

* **Set Up Inline Autocomplete (codegemma):**
  1. Go to IntelliJ **Settings** (`Cmd + ,`) ➡️ **Tools** ➡️ **DevoxxGenie** ➡️ **LLM Providers** (or **Completion** tab depending on plugin version build).
  2. Find the **Inline Code Completion / FIM Provider** block.
  3. Set the provider to `Ollama` and explicitly assign the model to `codegemma:2b`.

### 5. Verification

* Open a source file and begin typing.
* The `codegemma:2b` model handles quick inline autocompletions (press `Tab` to accept ghost text) throwing a `POST /api/generate` log entry in your terminal.
* Highlighting code and hitting `Cmd + L` or `Cmd + I` routes complex reasoning, refactoring, and code edits to the smarter `qwen2.5-coder:7b` model.
