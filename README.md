# hku-consent-form

A [Claude Code](https://claude.ai/code) skill that drafts informed consent forms in the format used by the University of Hong Kong Human Research Ethics Committee (HREC), from a research proposal.

Give it a proposal (and, if available, the HREC application form and interview protocol). It extracts the fields, picks the audiences that the study needs, fills in the standard HKU wording, and writes one `.docx` per audience and language.

## Audiences and formats

| Audience | Format |
|---|---|
| Adult participant / teacher | Sectioned (PURPOSE … SIGNATURE) |
| Teacher or professor, student researcher | Letter with reply slip |
| School principal | Letter with school reply slip |
| Parent / guardian | Sectioned, "your child" |
| Student assent | Letter, three registers (primary, S1–S3, S4–S6) |
| Oral / email consent | Short script |

English and Chinese. The Chinese script (Traditional for Hong Kong, Simplified for the Mainland) is chosen from the participant population described in the proposal.

## What is in the repo

- `SKILL.md` — the workflow Claude follows
- `reference/fields.md` — what to extract from the proposal, with defaults
- `reference/language-en.md`, `reference/language-zh.md` — sentence banks taken from HKU Faculty of Education sample forms and approved applications
- `reference/checklist.md` — consistency checks against the HREC application form before submission

Personal details of the principal investigator are not in the repo. Put them in `local/pi-defaults.md` (ignored by git); the skill reads that file when present.

## Requirements

[Pandoc](https://pandoc.org/) for the `.docx` output.

```bash
brew install pandoc
```

## Installation

```bash
git clone https://github.com/chinhsi/hku-consent-form.git ~/.claude/skills/hku-consent-form
```

Optional: create `~/.claude/skills/hku-consent-form/local/pi-defaults.md` with your name, title, department, phone and email.

## Usage

```
/hku-consent-form <proposal path or folder> [adult|teacher|principal|parent|student] [en|zh-hant|zh-hans|all]
```

The forms are drafts. Check them against your own application before submission; the HREC is the authority on wording.

## License

MIT
