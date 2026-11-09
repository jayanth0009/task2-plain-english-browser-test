# Five-minute demo recording script

Record one continuous walkthrough with the terminal and browser visible. Keep `.env` and API keys off screen.

## 0:00–0:30 — Overview

"This submission has two independent projects. Task 1 uses C# and Selenium to identify the requested fields by accessible meaning and context. Task 2 turns a plain-English test into a sequence of browser actions and checks the page after each step."

## 0:30–2:10 — Task 1

Show `Program.cs` and the environment options `FORM_URL`, `FIRST_NAME`, `GENDER` and `STATE`. From the Task 1 repository root, run:

```bash
FORM_URL="http://app.cloudqa.io/home/AutomationPracticeForm" FIRST_NAME="Jayanth" GENDER="Male" STATE="California" dotnet run
```

Explain that visible label, ARIA and nearby label context are scored and a tie stops execution. The URL and values are configurable. Mention that the matcher can fail if labels are removed or ambiguous.

## 2:10–4:20 — Task 2

Show `examples/phptravels.txt`; the URL and expected visible heading come from that test case. With dependencies installed and `.env` configured, run from the Task 2 repository root:

```bash
python src/runner.py --file examples/phptravels.txt --headed
```

Show the browser and PASS/action trace. Explain the supported action set and the fresh page snapshot after each action. Optionally run `python src/runner.py --file examples/generic-site.txt --headed` to show it is not tied to PHPTravels.

## 4:20–5:00 — Limits

"This is a prototype. The AI can misunderstand vague tests, custom widgets, dynamic pages and authentication. CAPTCHA or secrets need a person. Task 1 depends on meaningful labels. I would use the natural-language runner for exploration, then convert stable flows into reviewed deterministic tests. The PHPTravels example checks only the public page heading; it does not request access or send personal information."
