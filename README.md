# Task 2 — plain-English browser checks

An LLM-guided Playwright CLI. Give it a test case in everyday language; it observes the current page, chooses one action from a restricted set, executes it, and continues until it can verify success or reports failure/blocked. Site URLs come from the test case; PHPTravels is a demonstration, not a special case.

## Requirements

- Python 3.10
- OpenAI API key with access to the configured model
- Chromium installed for Playwright

## Setup

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
playwright install chromium
cp .env.example .env               # Windows: copy .env.example .env
```

Edit `.env` and set `OPENAI_API_KEY`. `OPENAI_MODEL` defaults to `gpt-4.1-mini`; choose a model available to your account. Never commit `.env` or a real key.

## Run

```bash
python src/runner.py --file examples/phptravels.txt --headed
python src/runner.py --test "Open https://example.org and verify the page shows Example Domain"
```

Exit code: 0 pass, 1 failed/blocked, 2 configuration error. `STEP_LIMIT` defaults to 12. Set `HEADLESS=true` to hide the browser; `--headed` shows it.

## Design and limitations

The model sees a compact page snapshot and selects from navigation, click, labeled fill/select, visibility assertions and URL assertions. Playwright executes one action at a time and reports the result back for the next decision. Actions use visible semantic labels/text and reject ambiguous targets. The model is instructed to treat page content as untrusted evidence and avoid destructive or financial actions.

This is a prototype, not a general autonomous QA engine. It can misunderstand vague tests, dynamic pages, custom widgets, authentication, CAPTCHA, localization, or deceptive page content. It does not prove correctness; assertions must be observable. LLM output can vary and API use costs money. The PHPTravels sample only checks the public demo heading; it does not create an account or submit personal details. For dependable regression coverage, convert stable flows into reviewed deterministic tests.
