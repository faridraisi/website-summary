# Website URL Summarizer

A Python tool that fetches a webpage, extracts meaningful text, and summarizes it using OpenAI's API.

Two notebooks are provided:
- **`summary_requests.ipynb`** — Uses `requests` (fast, lightweight, but blocked by some sites)
- **`summary_selenium.ipynb`** — Uses Selenium with headless Chrome (handles JavaScript-heavy and bot-protected sites)

## Setup

**Requirements:** Python 3.11+, [uv](https://docs.astral.sh/uv/), Chrome (for Selenium notebook)

```bash
git clone https://github.com/faridraisi/website-summary.git
cd website-summary
uv sync
cp .env.example .env
```

Edit `.env` and add your OpenAI API key:

```
OPENAI_API_KEY=sk-your-api-key-here
OPENAI_MODEL=gpt-4o-mini
```

## Usage

Open either notebook in VS Code or Jupyter, set the `url` variable, and run all cells.

### Requests version (lightweight)

Works with most websites. Will fail with a clear error message on sites that block automated requests (e.g. Cloudflare-protected sites).

### Selenium version (robust)

Launches a headless Chrome browser to render the page, including JavaScript. Handles sites that block simple HTTP requests. Uses `webdriver-manager` to automatically download the correct ChromeDriver — no manual driver setup needed.

## How it works

1. **Fetch** — Downloads the webpage (via `requests` or Selenium)
2. **Clean** — Strips non-content tags (script, style, nav, footer, etc.)
3. **Extract** — Pulls clean text, truncated to 15,000 characters
4. **Summarize** — Sends text to OpenAI API for a 3-5 paragraph summary

## Dependencies

| Package | Purpose |
|---------|---------|
| requests | HTTP requests (requests notebook) |
| beautifulsoup4 | HTML parsing and text extraction |
| openai | OpenAI API client |
| python-dotenv | Load API key from `.env` |
| selenium | Browser automation (Selenium notebook) |
| webdriver-manager | Auto-download matching ChromeDriver |
| ipykernel | Run notebooks in VS Code |
