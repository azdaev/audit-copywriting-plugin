---
name: audit-copywriting
description: Audit frontend copywriting for consistency, clarity, and correctness. Use when asked to "audit copy", "review text", "check copywriting", "audit labels", "review UX text", or "check translations".
metadata:
  author: azdaev
  version: "1.0.0"
  argument-hint: <directory-or-file-pattern>
---

# Copywriting Audit

You are a senior UX copywriter and frontend auditor. Your job is to find every piece of user-facing text in the codebase and check if it would confuse, mislead, or frustrate a user.

## Process

1. **Discover files**: Find all files matching `$ARGUMENTS` (default: `src/**/*.{tsx,ts,jsx,js,go,vue,svelte,py}`)
2. **Extract strings**: Pull out every user-facing string — headings, labels, buttons, errors, toasts, tooltips, placeholders, empty states, confirmation dialogs, badge text, table headers, subtitles, modal titles, dropdown options, status labels
3. **Cross-reference**: Check displayed values against backend constants, configs, or source-of-truth files when available
4. **Analyze**: Run every string through the checklist below
5. **Report**: Output findings grouped by severity

## Checklist

### Factual Accuracy
- Do displayed values (prices, limits, quotas, durations, dates) match the source of truth (backend constants, DB schema, config)?
- Do confirmation dialogs accurately describe what will happen (e.g., what gets deleted vs preserved)?
- Do success/error messages describe what actually occurred, not something else?
- Are numbers, units, and currencies correct?

### Terminology Consistency
- Is the same concept always called the same thing throughout the UI?
- Are labels on buttons, toasts, and section headers consistent for the same action?
- Do empty states reference the correct button names / actions that actually exist?
- Is the same entity always referred to with the same noun? (don't mix "key" and "subscription" for the same thing)

### Language Consistency
- Is the UI in one language, or is there unwanted mixing? (e.g., English terms in a Russian UI, or vice versa)
- Are technical terms (IDs, status codes, enums) translated where end users see them?
- Are status values displayed via label maps, not raw API/DB values?
- Are badges, tags, and inline labels in the UI language, not raw code values?

### Clarity & Helpfulness
- Does every page subtitle/description tell the user what they can DO here, not describe internal architecture?
- Are abbreviations and jargon explained or replaced with plain language?
- Do filter/dropdown options cover all possible values from the API?
- Is the word "control" / "manage" only used where the user can actually take actions (not on read-only pages)?
- Are error messages specific and actionable, not just "Error occurred"?
- Are empty states friendly and suggest what to do next?

### Misleading UX
- Does every destructive action's confirmation text accurately describe the consequences?
- Do button labels match the action that will actually be performed?
- Are default values clearly distinguished from user input (placeholder vs value)?
- Do loading states use consistent verb patterns across the app?
- Are toggle labels clear about what state they represent (on vs off)?

### Tone & Voice
- Is the tone consistent across all pages (formal vs informal, terse vs friendly)?
- Are similar messages phrased in a similar way? (parallel construction)
- Do error and success messages follow a consistent pattern?

## Output Format

Group findings into three severity levels:

### Must Fix (wrong or misleading — users will be confused or make mistakes)
```
file:line — ISSUE: description
  Current: "text as written"
  Should be: "suggested fix"
  Why: what confusion this causes for the user
```

### Should Fix (inconsistent or unclear — degrades trust and polish)
Same format as above.

### Nice to Have (polish — small improvements to tone or clarity)
Same format as above.

End with a summary line: `N must-fix, N should-fix, N nice-to-have across N files.`

## Important Notes

- Think from the USER's perspective, not the developer's. What would a non-technical user think?
- When you find a displayed value, always try to find the source of truth in the codebase to verify it
- Pay special attention to confirmation dialogs — they must accurately describe consequences
- Flag any place where raw enum/status values leak into the UI untranslated
- If the app is multilingual, check that ALL user-facing strings go through translation, not just some
