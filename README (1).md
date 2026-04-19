# Code Debugging Pair Agent

An AI-powered code debugger and reviewer built with the Anthropic Claude API. Acts as a senior software engineer pair programmer — paste any code and get a structured analysis in seconds.

## Features

- **Bug detection** — logical errors, runtime issues, type mismatches, concurrency problems
- **Edge case analysis** — null inputs, boundary values, unexpected data shapes
- **Severity-rated issues** — High / Medium / Low with clear explanations
- **Code fixes** — corrected snippets with reasoning for each fix
- **Refactored version** — improved, production-ready code with change notes
- **Engineering notes** — best practices, scalability, and design recommendations
- **Language support** — JavaScript, TypeScript, Python, Java, Go, Rust, C++, SQL, PHP, C#, Ruby, Bash, and more

## Demo

> Paste code → select language → hit **Analyze** → get structured results across 6 tabs.

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/code-debug-agent.git
cd code-debug-agent
```

### 2. Open the app

This is a single-file HTML app — no build step, no dependencies.

```bash
open code-debug-agent.html
# or just double-click the file
```

### 3. Add your API key

Enter your [Anthropic API key](https://console.anthropic.com) in the key field on the page. It is never stored — it only goes directly to Anthropic's API in your browser session.

## File Structure

```
code-debug-agent/
├── code-debug-agent.html   # The entire app (HTML + CSS + JS)
└── README.md
```

## How It Works

1. User pastes code into the editor
2. Optionally adds language, usage context, error messages, and expected behavior
3. On submit, the app calls `POST https://api.anthropic.com/v1/messages` directly from the browser
4. Claude responds with a structured JSON object
5. The UI parses and renders results across six tabs: Summary, Issues, Edge Cases, Fixes, Improved, Notes

### Prompt Design

The system prompt instructs Claude to return **pure JSON only** (no markdown fences, no preamble) matching this schema:

```json
{
  "summary": "string",
  "issues": [{ "title": "", "severity": "high|medium|low", "reason": "" }],
  "edge_cases": [{ "case": "", "behavior": "" }],
  "fixes": [{ "title": "", "explanation": "", "code": "" }],
  "improved": { "notes": "", "code": "" },
  "notes": ["string"]
}
```

## Configuration

| Setting | Where | Default |
|---|---|---|
| Model | `code-debug-agent.html` line with `model:` | `claude-sonnet-4-20250514` |
| Max tokens | Same file, `max_tokens:` | `3000` |
| API key | UI input field | — |

To change the model, open the HTML file and update:

```js
model: 'claude-sonnet-4-20250514',
```

## Keyboard Shortcut

Press **Ctrl+Enter** (or **Cmd+Enter** on Mac) inside the code editor to run the analysis.

## Security Note

- Your API key is **not stored** anywhere (no localStorage, no cookies, no server)
- It is sent only to `https://api.anthropic.com` directly from your browser
- Do not commit your API key into the repo

## Requirements

- A modern browser (Chrome, Firefox, Safari, Edge)
- An [Anthropic API key](https://console.anthropic.com)
- No Node.js, no build tools, no dependencies

## License

MIT
