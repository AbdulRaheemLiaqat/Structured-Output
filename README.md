# Structured JSON Output — Customer Support Classifier

## Objective

This project demonstrates structured LLM output by extracting customer-support information into predictable JSON.

The schema contains:

- `name`
- `email`
- `issue_type`
- `urgency`

## Files

- `schema.json` — JSON Schema used to constrain the model output.
- `prompt.txt` — prompt containing strict JSON-only instructions.
- `main.py` — validation tests and optional live LLM tests.
- `requirements.txt` — Python dependencies.
- `.env.example` — example environment variables; contains no real API key.
- `.gitignore` — prevents secrets and Python cache files from being committed.

## Setup

```bash
pip install -r requirements.txt
```

## Offline validation

This does not require an API key:

```bash
python main.py --offline
```

It parses and validates five sample JSON responses plus the deliberately messy-input result.

## Live LLM testing

1. Set your API key as an environment variable.
2. Optionally set `OPENAI_MODEL`.
3. Run:

```bash
python main.py --live
```

On Windows PowerShell:

```powershell
$env:OPENAI_API_KEY="your_key_here"
python main.py --live
```

Do not put a real API key into the repository.

## Deliberate break test

The messy input includes:

- emotional/noisy text,
- a malformed email,
- multiple issues,
- an instruction attempting to override the classifier.

The strengthened prompt treats the message as untrusted data and defines fallback behavior. The strict JSON schema also prevents extra fields and invalid enum values.

## Expected result

All five normal test cases should parse successfully. The messy case should also produce a schema-valid JSON object when using structured outputs.

## Concepts demonstrated

- Structured outputs / JSON mode
- JSON Schema design
- Prompt constraints
- API response parsing
- JSON validation
- Handling messy input
- Prompt-injection resistance
