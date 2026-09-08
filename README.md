# Nurix AI

Deployment-ready Flask + Google Gemini Interactions API chatbot.

## Project structure

```text
Nurix_AI_Deployment/
├── app.py
├── templates/
│   └── index.html
├── requirements.txt
├── .env.example
├── .gitignore
├── Procfile
└── README.md
```

## Local setup

1. Create a virtual environment:

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Create `.env` from `.env.example` and set your API key:

```env
GEMINI_API_KEY=your_real_key_here
GEMINI_MODEL=gemini-3.6-flash
MAX_HISTORY_MESSAGES=10
MAX_CONTENT_CHARS=50000
```

4. Start:

```bash
python app.py
```

Open `http://127.0.0.1:5000`.

## Production

Set `GEMINI_API_KEY` in your hosting provider's environment/secrets settings. Do not upload a real `.env` file.

Start command:

```bash
gunicorn --bind 0.0.0.0:$PORT --workers 1 --threads 4 --timeout 120 app:app
```

The app listens on the provider's `PORT` value.

## Important fix

`index.html` is inside `templates/` because Flask's `render_template("index.html")` searches that directory. Keeping the HTML at the project root causes a 500 error when `/` is opened.

## Health check

`/health` returns JSON and can be used by a hosting provider's health check.

## API key security

Never put the Gemini API key in frontend JavaScript or commit `.env`. If an API key has ever been exposed publicly, revoke it and create a replacement.

## Current feature scope

The frontend supports the existing chat UI, streaming responses, voice input, and attachment controls. Text from supported text files can be included in the conversation. Browser image previews are currently UI-only; server-side image understanding and PDF/DOCX extraction are not enabled in this version.
