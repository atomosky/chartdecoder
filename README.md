# Chart Decoder

A medical terminology game for health informatics students. Players learn Greek and Latin word parts in a **Bootcamp**, then decode realistic, **"de-identified" synthetic clinical notes** from 26 specialties and disciplines, including inpatient, outpatient, and emergency settings.

All cases are fictional teaching examples. They are not real patient data or clinical guidance.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole game in one file. All content (bootcamp terms and clinical cases) is in the block marked `CONTENT: edit cases & bootcamp terms below`. |
| `README.md` | This file. |

## Put it on GitHub Pages

1. Create a new repository (e.g., `chart-decoder`) and upload both files to the root.
2. Go to **Settings → Pages**, set Source to **Deploy from a branch**, then choose `main` / `(root)`.
3. After a minute or two, the game is live at `https://<your-username>.github.io/chart-decoder/`.

No build step or server is needed. It also runs if you double-click `index.html` locally or open it in a preview.

## Clinician review

Open the site with `#review` at the end of the URL (or click **Clinician review mode** in the footer). That page shows every note with its full answer key, distractors, and explanations, plus a printable comments box. Reviewers can use **Print / save as PDF** to mark it up.

When a case is approved, set it in the CONTENT block:

```js
reviewed: true, reviewedBy: "Jane Doe, MD",
```

Cases with `reviewed: false` show a "Draft, pending clinician review" label.

## Editing or adding a case

Each case in the CONTENT block looks like this:

```js
{ id: "cards-afib", specialty: "Cardiology", setting: "Outpatient",
  type: "Clinic Follow-up", title: "An irregular rhythm", reviewed: false,
  note: `Pt is a 67 y/o M seen in f/u for {AFib} ... Visit date: [[DATE]]`,
  qs: [
    ["AFib", "Atrial fibrillation", ["Acute febrile illness", "Aortic fibrosis", "Atrial flutter"], "Explanation shown after answering."]
  ]}
```

- `{term}` marks a quizzable term. The text inside the braces must exactly match the first item of a question.
- `[[TYPE]]` is a redaction. Valid types are `NAME`, `DATE`, `MRN`, `PROVIDER`, `HOSPITAL`, `LOCATION`, `PHONE`, `ACCOUNT`, and `AGE 90+`.
- `setting` must be `Inpatient`, `Outpatient`, or `Emergency` (these drive the filter chips).
- Each question needs exactly 3 wrong answers.
- For a concept question that isn't tied to a term, use `null` as the term and add a prompt, plus an optional redaction type to highlight:
  `[null, "answer", [3 wrongs], "explanation", "Question prompt?", "DATE"]`

Keep the backticks around `note` and the commas between cases. If the page goes blank after an edit, a missing comma or quote in the CONTENT block is the usual cause.

## Features

- **Bootcamp**: 5 sets (prefixes, roots, suffixes, Rx and Latin, chart shorthand), with flip cards and quizzes
- **28 notes / 192 questions** with explanations that break words into their parts
- **3 redaction styles** students can toggle: `___` (MIMIC-IV style), `[**Name**]` (MIMIC-III style), and black bars. Tapping a redaction explains which HIPAA identifier it is.
- **Context traps** that reappear across specialties (RA, AG, PD, ASA, STE, DME, HCP, and more)
- Hints, streak bonuses, stars, and a "plain-language" translated note at the end of each case
- Progress saved in the player's own browser (no accounts, no data collected)
- Keyboard play (1–4, H, Enter), mobile layout, and dark mode
